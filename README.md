# Universal Image Crawler & Preprocessor v2

Automated image collection and preprocessing pipeline for object detection tasks. Crawls images by category, filters quality, and outputs YOLO-compatible 640x640 images.

## Features

- External keyword management via `keywords.txt`
- Configurable crawling strategies
- Manual filtering support
- Automatic sequential renaming
- Quality filtering (blur, brightness, resolution)
- YOLO-compatible output with aspect ratio preservation

## Requirements

```bash
pip install icrawler opencv-python tqdm pillow
```

## Quick Start

### 1. Create keywords.txt

```
croissant
pizza
screwdriver
고구마 파이
```

### 2. Run Notebook

Execute `image_crawler_v2.ipynb` cells in order:

1. Setup directories and read keywords
2. Crawl images
3. Manual review: delete unwanted images from `raw_images_crawled/[category]/images/`
4. Rename to sequential format
5. Apply quality filters and resize

## Configuration

### Crawling Options (Cell 2)

```python
USE_KEYWORD_VARIATIONS = False  # Use multiple search variations
ADD_BREAD_SUFFIX = True         # Add "bread" to keywords
SKIP_CRAWLING = False          # Skip crawling, use existing images
```

**Recommended for stable crawling:**
```python
USE_KEYWORD_VARIATIONS = False
ADD_BREAD_SUFFIX = True
```

### Target Settings

```python
TARGET_IMAGES = 200           # Target images per category
MAX_IMAGES_PER_SEARCH = 150   # Max images per search
```

## Folder Structure

```
project/
├── keywords.txt
├── image_crawler_v2.ipynb
└── raw_images_crawled/
    ├── croissant/
    │   ├── images/           # Raw downloaded images
    │   └── processed/        # Filtered & resized (640x640)
    └── pizza/
        ├── images/
        └── processed/
```

## Troubleshooting

**Crawling errors or no images downloaded:**
- Enable VPN or wait 30-60 minutes
- Use English keywords when possible
- Set `SKIP_CRAWLING = True` and manually download images to `raw_images_crawled/[category]/images/`

**Poor search results:**
- Enable `ADD_BREAD_SUFFIX = True` for food items
- Use specific keywords in `keywords.txt`
- Try `USE_KEYWORD_VARIATIONS = True` for broader coverage

## Output

- **Raw images**: `raw_images_crawled/[category]/images/`
- **Processed images**: `raw_images_crawled/[category]/processed/`
- **Summary report**: Final count per category

```
Summary Report:
--------------------------------------------------
croissant: 45 processed images
pizza: 38 processed images
--------------------------------------------------
Total: 83 processed images
```
