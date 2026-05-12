
# Raw Pair Picker Pro

A professional local desktop tool for photographers to select JPG preview images and automatically export the matching RAW / JPG / XMP files by filename.

专业的 JPG + RAW 成组选片与导出工具。

---

## 1. Project Overview

Raw Pair Picker Pro is a local desktop application designed for photographers who shoot in both JPG and RAW formats.

Many cameras generate files like this:

```text
DSC01234.JPG
DSC01234.ARW
DSC01235.JPG
DSC01235.ARW
DSC01236.JPG
DSC01236.ARW
````

JPG files are lightweight and easy to preview, while RAW files are large and mainly used for final editing.

This app allows users to:

1. Open a folder containing both JPG and RAW files.
2. Preview only the JPG images.
3. Select, rate, or reject photos through a GUI.
4. Automatically find the matching RAW file with the same filename stem.
5. Export selected RAW / JPG / XMP files to a target folder.
6. Generate selection and export reports.

The original files are never modified, moved, or deleted.

---

## 2. Why This Project Exists

When shooting events, races, travel photos, portraits, or street photography, photographers often produce hundreds or thousands of JPG + RAW file pairs.

A common workflow problem is:

```text
I want to choose photos quickly by looking at JPG previews,
but I need to export the matching RAW files for editing.
```

Manual matching is slow and error-prone.

For example, after selecting:

```text
DSC00231.JPG
DSC00418.JPG
DSC00677.JPG
```

the user still has to manually find:

```text
DSC00231.ARW
DSC00418.ARW
DSC00677.ARW
```

Raw Pair Picker Pro automates this process.

---

## 3. Core Workflow

Recommended workflow:

```text
1. Shoot JPG + RAW in camera
2. Put all files in one source folder
3. Open the source folder in Raw Pair Picker Pro
4. Preview JPG files
5. Select / rate / reject photos
6. Choose an output folder
7. Export matching RAW / JPG / XMP files
8. Use exported RAW files for final editing
```

Example source folder:

```text
2026_F1_Shanghai/
├── DSC0001.JPG
├── DSC0001.ARW
├── DSC0002.JPG
├── DSC0002.ARW
├── DSC0003.JPG
├── DSC0003.ARW
```

After selecting `DSC0001.JPG` and `DSC0003.JPG`, the app exports:

```text
exported_raw/
├── DSC0001.ARW
├── DSC0003.ARW
├── selected_list.csv
├── export_report.txt
```

---

## 4. Key Features

### 4.1 Folder Scanning

The app scans a selected source folder and displays only JPG preview files.

Supported JPG formats:

```text
.jpg
.jpeg
.JPG
.JPEG
```

Files are sorted by filename to preserve camera shooting order.

---

### 4.2 RAW File Matching

For every JPG file, the app searches for a RAW file with the same filename stem.

Example:

```text
DSC01234.JPG -> DSC01234.ARW
IMG_8821.JPG -> IMG_8821.CR3
P1000234.JPG -> P1000234.RW2
```

Supported RAW formats:

```text
.ARW / .arw    Sony
.CR3 / .cr3    Canon
.CR2 / .cr2    Canon
.NEF / .nef    Nikon
.RAF / .raf    Fujifilm
.DNG / .dng    Adobe DNG
.RW2 / .rw2    Panasonic
.ORF / .orf    Olympus
```

---

### 4.3 XMP Sidecar Detection

The app can detect optional XMP sidecar files.

Example:

```text
DSC01234.JPG
DSC01234.ARW
DSC01234.XMP
```

When export mode includes XMP, the matching `.XMP` file will also be copied.

---

### 4.4 Thumbnail Grid

The main interface displays JPG files in a scrollable thumbnail grid.

Each thumbnail card shows:

```text
- Image preview
- Filename
- Selection checkbox
- Star rating
- RAW status
```

Example card information:

```text
DSC01234.JPG
Rating: ★★★★☆
Selected: Yes
RAW: Found
```

---

### 4.5 Large Preview Panel

Clicking a thumbnail opens a larger preview.

The preview panel displays:

```text
- Large JPG preview
- Filename
- Selected status
- Rating
- Rejected status
- RAW path
- XMP path
```

This helps users check focus, composition, motion blur, and expression before exporting RAW files.

---

### 4.6 Selection System

Users can mark photos as selected.

Selection is independent from rating.

This means a photo can be:

```text
Selected but unrated
Rated but not selected
Rejected
Selected and rated
```

This design supports flexible photography workflows.

---

### 4.7 Star Rating System

Users can assign ratings from 1 to 5 stars.

Rating examples:

```text
1 star  - weak candidate
2 stars - usable
3 stars - good
4 stars - strong
5 stars - final pick
```

The app can export images based on rating thresholds.

Supported export conditions:

```text
Selected only
Rating >= 3
Rating >= 4
Rating = 5
```

---

### 4.8 Reject System

Users can mark photos as rejected without deleting them.

Rejected files are only marked inside the app state.

The original files remain untouched.

This is useful for:

```text
- Out-of-focus photos
- Bad exposure
- Duplicate shots
- Bad composition
- Unwanted expressions
```

---

### 4.9 Filters

The app supports multiple filter modes:

```text
All
Selected
Rejected
Unrated
Rating >= 3
Rating >= 4
Rating = 5
Missing RAW
```

This makes it easier to manage large photo folders.

---

### 4.10 Export Modes

The app supports different export modes:

```text
RAW only
RAW + JPG
RAW + JPG + XMP
```

Recommended default:

```text
RAW + JPG
```

Reason:

```text
RAW is used for editing.
JPG is useful as a visual reference.
```

---

### 4.11 Duplicate Handling

By default, existing files in the output folder are skipped.

This prevents accidental overwriting.

Supported duplicate handling modes:

```text
Skip existing files
Overwrite existing files
Rename duplicated files
```

Recommended default:

```text
Skip existing files
```

---

### 4.12 State Persistence

Selection state is automatically saved inside the source folder:

```text
.selected_cache/state.json
```

The state file records:

```json
{
  "DSC01234.JPG": {
    "selected": true,
    "rating": 5,
    "rejected": false
  }
}
```

When the same folder is opened again, the app restores the previous selection state.

This allows users to continue selecting photos over multiple sessions.

---

### 4.13 Thumbnail Cache

Generated thumbnails are cached in:

```text
.selected_cache/thumbnails/
```

This improves loading speed when opening the same folder again.

The cache system prevents unnecessary thumbnail regeneration.

---

### 4.14 Export Reports

After export, the app generates several reports.

#### `selected_list.csv`

Records all selected or exported files.

Columns:

```csv
filename,stem,selected,rating,rejected,raw_found,jpg_path,raw_path,xmp_path,exported
```

Example:

```csv
filename,stem,selected,rating,rejected,raw_found,jpg_path,raw_path,xmp_path,exported
DSC01234.JPG,DSC01234,true,5,false,true,D:/Photos/DSC01234.JPG,D:/Photos/DSC01234.ARW,D:/Photos/DSC01234.XMP,true
```

#### `export_report.txt`

Summarizes the export operation.

Example:

```text
Export Report
=============

Source folder: D:/Photos/2026_F1
Output folder: D:/Photos/Selected_RAW

Total JPG files: 420
Selected files: 38
Exported RAW files: 38
Missing RAW files: 0
Skipped existing files: 2
Export mode: RAW + JPG
```

#### `missing_raw.txt`

Generated only when some selected JPG files do not have matching RAW files.

Example:

```text
Missing RAW Files
=================

DSC00882.JPG
DSC00941.JPG
```

---

## 5. Keyboard Shortcuts

The app supports fast keyboard-based selection.

| Shortcut    | Action                          |
| ----------- | ------------------------------- |
| Left Arrow  | Previous image                  |
| Right Arrow | Next image                      |
| Space       | Toggle selected                 |
| 1           | Set rating to 1 star            |
| 2           | Set rating to 2 stars           |
| 3           | Set rating to 3 stars           |
| 4           | Set rating to 4 stars           |
| 5           | Set rating to 5 stars           |
| 0           | Clear rating                    |
| X           | Toggle rejected                 |
| U           | Unreject current photo          |
| Ctrl + S    | Save current state              |
| Ctrl + E    | Export selected files           |
| Esc         | Clear focus / exit preview mode |

These shortcuts are designed for fast photo culling.

---

## 6. Safety Guarantees

Raw Pair Picker Pro is designed to be non-destructive.

The app will never:

```text
- Delete original files
- Move original files
- Rename original files
- Modify original JPG files
- Modify original RAW files
- Modify original XMP files
```

The app only:

```text
- Reads source files
- Generates thumbnails
- Saves selection state
- Copies selected files to the output folder
- Generates reports
```

This makes the workflow safe for original photography archives.

---

## 7. Project Structure

```text
raw-pair-picker-pro/
│
├── README.md
├── requirements.txt
├── run.py
├── .gitignore
│
├── src/
│   └── raw_pair_picker/
│       │
│       ├── __init__.py
│       ├── main.py
│       ├── config.py
│       │
│       ├── domain/
│       │   ├── __init__.py
│       │   ├── models.py
│       │   └── constants.py
│       │
│       ├── services/
│       │   ├── __init__.py
│       │   ├── folder_scanner.py
│       │   ├── raw_matcher.py
│       │   ├── thumbnail_cache.py
│       │   ├── state_store.py
│       │   ├── exporter.py
│       │   └── report_writer.py
│       │
│       ├── ui/
│       │   ├── __init__.py
│       │   ├── main_window.py
│       │   ├── toolbar.py
│       │   ├── thumbnail_grid.py
│       │   ├── preview_panel.py
│       │   ├── status_panel.py
│       │   └── dialogs.py
│       │
│       └── utils/
│           ├── __init__.py
│           ├── file_utils.py
│           └── logger.py
│
├── tests/
│   ├── test_raw_matcher.py
│   ├── test_folder_scanner.py
│   └── test_exporter.py
│
└── docs/
    ├── workflow.md
    └── shortcuts.md
```

---

## 8. Architecture Design

The project separates GUI code from business logic.

This makes the app easier to maintain, test, and extend.

### 8.1 Domain Layer

Location:

```text
src/raw_pair_picker/domain/
```

Responsible for data models and constants.

Main model:

```python
@dataclass
class PhotoItem:
    jpg_path: Path
    stem: str
    raw_path: Optional[Path]
    xmp_path: Optional[Path]
    selected: bool = False
    rejected: bool = False
    rating: int = 0
    raw_found: bool = False
```

---

### 8.2 Services Layer

Location:

```text
src/raw_pair_picker/services/
```

Responsible for core logic.

| Module               | Responsibility                        |
| -------------------- | ------------------------------------- |
| `folder_scanner.py`  | Scan source folder and find JPG files |
| `raw_matcher.py`     | Match JPG files with RAW / XMP files  |
| `thumbnail_cache.py` | Generate and load cached thumbnails   |
| `state_store.py`     | Save and restore selection state      |
| `exporter.py`        | Copy selected files to output folder  |
| `report_writer.py`   | Generate CSV and text reports         |

---

### 8.3 UI Layer

Location:

```text
src/raw_pair_picker/ui/
```

Responsible for PySide6 interface.

| Module              | Responsibility                    |
| ------------------- | --------------------------------- |
| `main_window.py`    | Main application window           |
| `toolbar.py`        | Top control bar                   |
| `thumbnail_grid.py` | Scrollable thumbnail grid         |
| `preview_panel.py`  | Large image preview               |
| `status_panel.py`   | Bottom statistics and status      |
| `dialogs.py`        | Export dialogs and error messages |

---

### 8.4 Utils Layer

Location:

```text
src/raw_pair_picker/utils/
```

Responsible for shared helper functions.

| Module          | Responsibility                  |
| --------------- | ------------------------------- |
| `file_utils.py` | File path and extension helpers |
| `logger.py`     | Application logging             |

---

## 9. Installation

### 9.1 Requirements

Recommended environment:

```text
Python 3.10+
Windows 10 / Windows 11
```

Python packages:

```text
PySide6
Pillow
pytest
```

---

### 9.2 Clone the Project

```bash
git clone https://github.com/your-username/raw-pair-picker-pro.git
cd raw-pair-picker-pro
```

---

### 9.3 Create Virtual Environment

Windows PowerShell:

```bash
python -m venv .venv
.venv\Scripts\activate
```

Windows CMD:

```bash
python -m venv .venv
.venv\Scripts\activate.bat
```

macOS / Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

### 9.4 Install Dependencies

```bash
pip install -r requirements.txt
```

Example `requirements.txt`:

```text
PySide6>=6.6.0
Pillow>=10.0.0
pytest>=7.0.0
```

---

## 10. How to Run

From the project root directory:

```bash
python run.py
```

The application window should open.

---

## 11. How to Use

### Step 1: Open Source Folder

Click:

```text
Open Source Folder
```

Choose the folder containing both JPG and RAW files.

Example:

```text
D:/Photos/2026_F1_Shanghai/
```

---

### Step 2: Review JPG Images

The app displays JPG thumbnails.

Click any thumbnail to preview it in the large preview panel.

---

### Step 3: Select Photos

Use the checkbox or keyboard shortcut:

```text
Space
```

to select or unselect the current photo.

---

### Step 4: Rate Photos

Use number keys:

```text
1, 2, 3, 4, 5
```

to assign star ratings.

Use:

```text
0
```

to clear the rating.

---

### Step 5: Reject Photos

Use:

```text
X
```

to mark the current photo as rejected.

Use:

```text
U
```

to remove the rejected mark.

---

### Step 6: Choose Output Folder

Click:

```text
Choose Output Folder
```

Select where exported files should be copied.

Example:

```text
D:/Photos/Selected_RAW/
```

---

### Step 7: Choose Export Mode

Available export modes:

```text
RAW only
RAW + JPG
RAW + JPG + XMP
```

Recommended:

```text
RAW + JPG
```

---

### Step 8: Export

Click:

```text
Export
```

or press:

```text
Ctrl + E
```

The app will copy matching files to the output folder and generate reports.

---

## 12. Example Use Case

A photographer shoots a motorsport event with Sony A6700.

The camera creates:

```text
DSC04501.JPG
DSC04501.ARW
DSC04502.JPG
DSC04502.ARW
DSC04503.JPG
DSC04503.ARW
```

The user opens the folder in Raw Pair Picker Pro.

The user selects:

```text
DSC04501.JPG
DSC04503.JPG
```

The app exports:

```text
DSC04501.ARW
DSC04503.ARW
```

If export mode is `RAW + JPG`, the app exports:

```text
DSC04501.ARW
DSC04501.JPG
DSC04503.ARW
DSC04503.JPG
```

---

## 13. Testing

Run all tests:

```bash
pytest
```

Run a specific test file:

```bash
pytest tests/test_raw_matcher.py
```

Recommended test coverage:

```text
- JPG scanning
- RAW matching
- Missing RAW detection
- XMP detection
- Export copy logic
- Skip existing files logic
- State save and restore logic
```

---

## 14. Build Windows Executable

The app can be packaged into a Windows executable with PyInstaller.

Install PyInstaller:

```bash
pip install pyinstaller
```

Build command:

```bash
pyinstaller --noconsole --name RawPairPickerPro run.py
```

Output location:

```text
dist/RawPairPickerPro/
```

Run:

```text
RawPairPickerPro.exe
```

Recommended future build script:

```bash
python build_exe.py
```

---

## 15. Common Problems

### Problem 1: No JPG files found

Possible causes:

```text
- The selected folder does not contain JPG/JPEG files.
- Images are inside subfolders.
- File extensions are not .jpg or .jpeg.
```

Solution:

```text
Check the source folder and make sure JPG files are directly inside it.
```

---

### Problem 2: RAW files are missing

Possible causes:

```text
- Camera was set to RAW only.
- Camera was set to JPG only.
- JPG and RAW filenames do not match.
- RAW files are in another folder.
```

Example mismatch:

```text
DSC01234.JPG
_DSC01234.ARW
```

These two names do not have the same filename stem, so automatic matching may fail.

---

### Problem 3: Some thumbnails do not load

Possible causes:

```text
- Corrupted JPG file
- Unsupported image file
- Permission issue
```

Solution:

```text
Open the image manually to verify it is readable.
```

---

### Problem 4: App is slow with thousands of photos

Cause:

```text
Large folders require many thumbnails to be generated.
```

Recommended optimization:

```text
- Use thumbnail cache
- Use lazy loading
- Use background threads
- Avoid loading all full-size images at once
```

---

## 16. Development Roadmap

### Version 1.0 - MVP

Core features:

```text
- Open source folder
- Scan JPG files
- Match RAW files
- Display thumbnails
- Select photos
- Export matching RAW files
- Generate selected_list.csv
```

---

### Version 1.1 - Better Selection Workflow

Planned features:

```text
- Large preview panel
- Star rating
- Reject mark
- Save and restore selection state
- Keyboard shortcuts
```

---

### Version 1.2 - Professional Export System

Planned features:

```text
- Export RAW only
- Export RAW + JPG
- Export RAW + JPG + XMP
- Export by rating threshold
- Missing RAW report
- Export report
```

---

### Version 1.3 - Performance Optimization

Planned features:

```text
- Lazy thumbnail loading
- Background scanning
- Progress bar
- Cancel loading button
- Thumbnail cache validation
```

---

### Version 1.4 - Packaging

Planned features:

```text
- Windows executable build
- PyInstaller packaging
- App icon
- Installer
```

---

## 17. Design Principles

This project follows several important design principles:

### 17.1 Non-destructive Workflow

Original files are protected.

The app copies files only.

---

### 17.2 Filename-based Matching

The app relies on filename stems.

Example:

```text
DSC01234.JPG
DSC01234.ARW
```

Both files share:

```text
DSC01234
```

This is the matching key.

---

### 17.3 Separation of Concerns

GUI code should not directly contain file operation logic.

Good:

```text
UI calls Exporter service
Exporter handles file copying
ReportWriter handles reports
```

Bad:

```text
Button click function directly scans, matches, copies, and writes reports
```

---

### 17.4 Recoverable State

User selection should not disappear after closing the app.

Selection state is saved locally and can be restored.

---

### 17.5 Scalable Workflow

The app should support both:

```text
Small folder: 50 photos
Large folder: 5000 photos
```

Performance optimization should focus on lazy loading and caching.

---

## 18. Limitations

Current filename-based matching requires JPG and RAW files to share the same filename stem.

This works well for most camera workflows.

However, automatic matching may fail when:

```text
- Files were renamed incorrectly
- JPG and RAW were exported from different software
- Camera created different naming rules
- RAW files are stored in another folder
- Duplicate filename stems exist
```

Future versions may support advanced matching by:

```text
- Capture time
- EXIF timestamp
- File size
- User-defined matching rules
```

---

## 19. Future Improvements

Possible future features:

```text
- EXIF metadata display
- Focus check zoom mode
- Compare two images side by side
- Batch rename after export
- Support subfolder scanning
- Support multiple source folders
- Dark mode
- Contact sheet export
- Lightroom collection export
- Drag-and-drop folder loading
- Automatic backup before export
- AI-assisted blurry image detection
```

---

## 20. License

This project is intended for personal learning and photography workflow automation.

Recommended license:

```text
MIT License
```

---

## 21. Project Status

Current target:

```text
Build a complete working MVP first.
```

Recommended implementation order:

```text
1. Folder scanning
2. RAW matching
3. Basic GUI
4. Thumbnail grid
5. Selection system
6. Export system
7. Reports
8. State persistence
9. Rating and filtering
10. Performance optimization
11. Windows packaging
```
