# 🖼️ Universal Image Crawler & Preprocessor v2

This project automates the collection and preprocessing of categorized images for use in object detection tasks (e.g., YOLO). Version 2 includes external keyword management, enhanced crawling strategies, and improved error handling.

## 📌 Features

### Core Features
- **External keyword management**: Define categories in `keywords.txt` file
- **Flexible crawling strategies**: Choose between original keywords or keyword variations
- **Enhanced error handling**: Multiple fallback strategies for robust crawling
- **Smart keyword processing**: Optional "bread" suffix addition for better search results
- **Manual filtering support**: Review and delete unwanted images before processing
- **Automatic renaming**: Sequential naming (`0000.jpg`, `0001.jpg`, ...)
- **Quality filtering**: Remove blurry, dark, or low-resolution images
- **YOLO-compatible output**: Resize to 640x640 with aspect ratio preservation

### New in v2
- **External keyword file**: Manage categories via `keywords.txt`
- **Configurable crawling options**: Control keyword variations and search strategies
- **Improved stability**: Better error handling and fallback mechanisms
- **Enhanced preprocessing**: More sophisticated image quality filters
- **Progress tracking**: Detailed reports and progress indicators

## 🛠️ Requirements

Install dependencies:

```bash
pip install icrawler opencv-python tqdm pillow
```

## 🚀 Quick Start

### 1. Setup Keywords
Create a `keywords.txt` file in your project directory with one keyword per line:

```
croissant
고구마 파이
소보로 빵
screwdriver
apple
```

### 2. Run the Notebook
Execute cells in `image_crawler_v2.ipynb` sequentially:

1. **Cell 1**: Setup directories and read keywords
2. **Cell 2**: Crawl images (configurable options)
3. **Manual Review**: Inspect and delete unwanted images
4. **Cell 3**: Rename images to sequential format
5. **Cell 4**: Define preprocessing functions
6. **Cell 5**: Apply quality filters and resize images

## ⚙️ Configuration Options

### Cell 2 Crawling Configuration

```python
# Configuration options in Cell 2
USE_KEYWORD_VARIATIONS = False  # Enable/disable keyword variations
ADD_BREAD_SUFFIX = True         # Add "bread" to keywords for better results
SKIP_CRAWLING = False          # Skip crawling entirely (use existing images)
```

### Crawling Strategies

| Setting | Description | Example |
|---------|-------------|---------|
| `USE_KEYWORD_VARIATIONS = True` | Use multiple search variations | "apple" → "apple", "apple bread", "apple bakery", "fresh apple", "apple food" |
| `USE_KEYWORD_VARIATIONS = False, ADD_BREAD_SUFFIX = True` | Add "bread" suffix only | "apple" → "apple bread" |
| `USE_KEYWORD_VARIATIONS = False, ADD_BREAD_SUFFIX = False` | Use original keywords only | "apple" → "apple" |

### Target Settings

```python
TARGET_IMAGES = 200           # Target number of images per category
MAX_IMAGES_PER_SEARCH = 150   # Maximum images per individual search
```

## 📁 Folder Structure

After running the complete pipeline:

```
project/
├── keywords.txt                    # Your category definitions
├── image_crawler_v2.ipynb         # Main notebook
├── raw_images_crawled/
│   ├── croissant/
│   │   ├── images/                 # Raw downloaded images
│   │   │   ├── 0000.jpg
│   │   │   ├── 0001.jpg
│   │   │   └── ...
│   │   └── processed/              # Quality-filtered & resized images
│   │       ├── 0000.jpg
│   │       ├── 0001.jpg
│   │       └── ...
│   ├── 고구마_파이/
│   │   ├── images/
│   │   └── processed/
│   └── ...
```

## 🔧 Detailed Usage

### Step 1: Keywords Setup
Create `keywords.txt` with your desired categories:
```
# Food items
croissant
pizza
hamburger

# Tools
screwdriver
hammer
wrench

# Korean items (supported)
고구마 파이
단팥빵
```

### Step 2: Image Crawling
Configure and run Cell 2:

**For stable crawling (recommended):**
```python
USE_KEYWORD_VARIATIONS = False
ADD_BREAD_SUFFIX = True
SKIP_CRAWLING = False
```

**For maximum coverage:**
```python
USE_KEYWORD_VARIATIONS = True
ADD_BREAD_SUFFIX = False
SKIP_CRAWLING = False
```

**To skip crawling (use existing images):**
```python
SKIP_CRAWLING = True
```

### Step 3: Manual Review
After crawling, manually review downloaded images:
1. Navigate to `raw_images_crawled/[category]/images/`
2. Delete irrelevant or poor-quality images
3. Keep only images you want to use for training

### Step 4: Automated Processing
Run Cells 3-5 to:
- Rename images to sequential format
- Apply quality filters (blur, brightness, content detection)
- Resize to 640x640 for YOLO compatibility
- Save processed images to `processed/` folder

## 🚨 Troubleshooting

### Common Issues

**1. Crawling Errors (`TypeError: 'NoneType' object is not iterable`)**
- Google may be blocking requests
- Try: Enable VPN, wait 30-60 minutes, or use English keywords
- Fallback: Set `SKIP_CRAWLING = True` and manually download images

**2. No Images Downloaded**
- Check internet connection
- Try different keywords (English keywords work better)
- Reduce `TARGET_IMAGES` to 50-100

**3. Poor Search Results**
- Enable `ADD_BREAD_SUFFIX = True` for food items
- Use more specific keywords in `keywords.txt`
- Try `USE_KEYWORD_VARIATIONS = True` for broader coverage

### Alternative Solutions

**Manual Download Method:**
1. Set `SKIP_CRAWLING = True` in Cell 2
2. Manually download images from Google Images
3. Save to `raw_images_crawled/[category]/images/`
4. Run Cells 3-5 for processing

**Keyword Optimization:**
```
# Good keywords
croissant bread
pizza slice
sweet potato pie

# Less effective
고구마 파이 (may be blocked)
very specific long phrases
```

## 📊 Output

The pipeline generates:
- **Raw images**: Original downloaded images in `images/` folders
- **Processed images**: Quality-filtered, 640x640 images in `processed/` folders
- **Summary report**: Final count of successfully processed images per category

### Processing Statistics
The final output includes detailed statistics:
```
Summary Report:
--------------------------------------------------
croissant: 45 processed images
pizza: 38 processed images
고구마 파이: 23 processed images
--------------------------------------------------
Total: 106 processed images
```

## 🔄 Version Differences

| Feature | v1 | v2 |
|---------|----|----|
| Keyword Management | Hardcoded in notebook | External `keywords.txt` file |
| Crawling Strategy | Single keyword + "bread" | Configurable variations |
| Error Handling | Basic | Enhanced with fallbacks |
| Progress Tracking | Minimal | Detailed reports |
| Image Quality Filters | Basic blur detection | Advanced multi-criteria filtering |
| Preprocessing | Simple resize | Aspect-ratio preserving with padding |

## 📝 Tips for Best Results

1. **Use English keywords when possible** - better crawling success rate
2. **Start with small targets** - try 50 images first, then scale up
3. **Review manually** - always inspect downloaded images before processing
4. **Use specific terms** - "chocolate croissant" vs "pastry"
5. **Enable bread suffix for food items** - improves search relevance
6. **Be patient** - add delays between requests to avoid blocking

## 📄 License

This project is open source and available under the MIT License.