# File Sorter

A simple Python script that organizes the files in a folder into category subfolders based on their file extension. Point it at a messy folder (like your Downloads), and it sorts every file into tidy folders like `Images`, `Documents`, `Videos`, and so on.

## Features

- Sorts files into categories based on their extension
- Automatically creates category folders as needed
- Skips folders and only moves actual files
- Sends anything it doesn't recognize to an `Other` folder
- Prints each move as it happens so you can see what it did

## Categories

Files are sorted according to the following extension map:

| Category    | Extensions                                              |
|-------------|---------------------------------------------------------|
| Images      | `.jpg` `.jpeg` `.png` `.gif` `.bmp` `.svg` `.webp`      |
| Documents   | `.pdf` `.doc` `.docx` `.txt` `.xlxs` `.pptx` `.csv`     |
| Videos      | `.mp4` `.mov` `.avi` `.mkv` `.wmv`                       |
| Audio       | `.mp3` `.wav` `.flac` `.aac` `.ogg`                      |
| Archives    | `.zip` `.rar` `.7z` `.tar` `.gz`                         |
| Code        | `.py` `.js` `.html` `.css` `.java` `.cpp`               |
| Other       | Anything not matched above                               |

## Requirements

- Python 3.x
- No external dependencies — it uses only the standard library (`os` and `shutil`)

## Usage

1. Run the script:

   ```bash
   python file_sorter.py
   ```

2. When prompted, enter the full path of the folder you want to sort:

   ```
   Enter the folder path to sort: /Users/you/Downloads
   ```

3. The script moves each file into a category subfolder inside that same folder and prints its progress:

   ```
   Moved: vacation.jpg → Images
   Moved: resume.pdf → Documents
   Moved: song.mp3 → Audio
   ```

## How it works

1. Prompts you for a folder path and lists everything inside it.
2. For each item, it skips anything that isn't a file (so existing subfolders are left alone).
3. It reads the file's extension (case-insensitive) and finds the matching category, defaulting to `Other` if there's no match.
4. It creates the destination category folder if it doesn't already exist, then moves the file in.

Because category folders are created inside the target folder and the script ignores folders, you can safely run it again on the same folder later to sort newly added files.

## Notes and limitations

- **No path validation.** If you enter a folder path that doesn't exist, the script will raise an error and stop.
- **Name collisions.** If a file with the same name already exists in the destination category folder, `shutil.move` may overwrite it or raise an error depending on your operating system. There's no duplicate-handling logic.
- **Excel extension typo.** The `Documents` category lists `.xlxs`, but the correct Excel extension is `.xlsx`. As written, real `.xlsx` files will end up in `Other`. To fix this, change `.xlxs` to `.xlsx` in the `FILE_CATEGORIES` dictionary.
- **Subfolders aren't sorted recursively.** Only files in the top level of the chosen folder are moved; files nested inside subfolders are left where they are.

## Customizing

To add new file types or categories, edit the `FILE_CATEGORIES` dictionary at the top of the script. For example, to add a `Fonts` category:

```python
FILE_CATEGORIES = {
    # ...existing categories...
    "Fonts": [".ttf", ".otf", ".woff", ".woff2"],
}
```
