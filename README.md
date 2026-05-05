# CR2 to JPG/HEIC Converter

Batch-converts Canon CR2 raw image files to JPG or HEIC format on Windows, using `dcraw` for raw processing and `exiftool` for metadata preservation.

---

## Contents

```
CR2-To-JPG-Converter/
├── cr2tojpg.sh          # Convert CR2 files to JPG
├── cr2toheic.sh         # Convert CR2 files to HEIC
├── dcraw.exe            # Raw image decoder
├── exiftool.exe         # Metadata extraction/transfer tool
├── libjpeg-62.dll       # Required DLL for JPEG support
├── exiftool_files/      # Supporting files for exiftool.exe
└── raw-photos/          # Drop your CR2 files here (or use your own folder)
```

---

## Requirements

- **Windows** with a Bash environment (e.g. [Git Bash](https://git-scm.com/downloads) or WSL)
- **ImageMagick** installed and available on your PATH
  - The JPG script uses `magick` (ImageMagick 7+)
  - The HEIC script uses `convert` (ImageMagick 6)
  - Download at: https://imagemagick.org/script/download.php

All other dependencies (`dcraw.exe`, `exiftool.exe`, and required DLLs) are bundled in this folder.

---

## Usage

Open Git Bash (or your Bash environment) and navigate to the converter folder:

```bash
cd /path/to/CR2-To-JPG-Converter
```

### Convert CR2 to JPG

```bash
./cr2tojpg.sh /path/to/your/cr2/folder
```

Converted files are saved to a new `output_jpg/` subfolder inside the folder you provided.

### Convert CR2 to HEIC

```bash
./cr2toheic.sh /path/to/your/cr2/folder
```

Converted files are saved to a new `output_heic/` subfolder inside the folder you provided.

---

## What the scripts do

1. Scan the provided folder for `.CR2` files
2. Decode each raw file using `dcraw` with 16-bit color depth and AHD interpolation
3. Pipe the decoded image through ImageMagick for final encoding (95% quality for JPG, 60% quality for HEIC)
4. Copy all Exif metadata from the original CR2 file to the output image using `exiftool`
5. Skip any file that has already been converted (won't overwrite existing output)
6. Print a timing summary when done

---

## Notes

- Only `.CR2` files (uppercase extension) are matched. Rename any lowercase `.cr2` files before running.
- The scripts must be run from the converter folder so that `dcraw.exe` and `exiftool.exe` are found correctly.
- HEIC encoding requires ImageMagick to be built with HEIC/HEVC support. If conversion fails, check that your ImageMagick install includes it.

---

## Third-party components

| Component | Source |
|-----------|--------|
| `dcraw` | https://www.dechifro.org/dcraw/ |
| `exiftool` | https://exiftool.org/ (Phil Harvey) |
| ExifTool Windows package | https://oliverbetz.de/pages/Artikel/ExifTool-for-Windows (Oliver Betz) |
| Strawberry Perl (bundled with exiftool) | https://strawberryperl.com/ |
