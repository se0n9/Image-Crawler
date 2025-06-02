# 🖼️ Universal Image Crawler & Preprocessor

This project automates the collection and preprocessing of categorized images for use in object detection tasks (e.g., YOLO).

## 📌 Features

- Define your own image categories (e.g., bread types, fruits, tools)
- Crawl up to 200 images per category using Google Images
- Manual filtering supported before preprocessing
- Automatic renaming (`0000.jpg`, `0001.jpg`, ...)
- Filter out blurry or low-resolution images
- Resize to 640x640 for YOLO-compatible training

## 🛠️ Requirements

Install dependencies:

```bash
pip install icrawler opencv-python tqdm pillow
```

## 🚀 Usage

1. Edit the list of `categories` (previously `bread_types`) in the notebook.
2. Run each step:
   - Step 1: Set up base and category directories
   - Step 2: Crawl images using keywords
   - Step 2.5: Manually review and delete unwanted images
   - Step 2.5: Rename remaining images
   - Step 3 & 4: Filter and resize for training

3. Folder structure:
```
raw_images_crawled/
├── croissant/
│   └── images/
│       ├── 0000.jpg
│       ├── ...
├── screwdriver/
│   └── images/
...
```

