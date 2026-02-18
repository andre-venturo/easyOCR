# EasyOCR Docker

Dockerized [EasyOCR](https://github.com/JaidedAI/EasyOCR) — end-to-end multi-lingual OCR solution.

## Build

```bash
docker build -t easyocr .
```

## Run

### Interactive Python shell

```bash
docker run --gpus all -it easyocr
```

```python
import easyocr
reader = easyocr.Reader(['en'])
result = reader.readtext('image.jpg')
print(result)
```

### CPU-only mode

```bash
docker run -it easyocr
```

```python
import easyocr
reader = easyocr.Reader(['en'], gpu=False)
result = reader.readtext('image.jpg')
print(result)
```

### CLI usage

Mount a directory with your images and run `easyocr` directly:

```bash
docker run --gpus all -v $(pwd)/seeds:/data easyocr \
  easyocr -l ch_sim en -f /data/chinese.jpg --detail=1 --gpu=True
```

CPU-only:

```bash
docker run -v $(pwd)/seeds:/data easyocr \
  easyocr -l en -f /data/image.png --detail=1 --gpu=False
```

### Interactive Python shell

Mount a directory containing your images into the container:

```bash
docker run --gpus all -it -v $(pwd)/seeds:/data easyocr
```

```python
import easyocr
reader = easyocr.Reader(['en'])
result = reader.readtext('/data/my_image.png')
print(result)
```

### Persist downloaded models

EasyOCR downloads language models on first use. Mount a volume to cache them across runs:

```bash
docker run --gpus all -it -v $(pwd)/models:/root/.EasyOCR/model easyocr
```

## Supported Languages

EasyOCR supports 80+ languages. Specify them when creating the reader:

```python
# English + Chinese Simplified
reader = easyocr.Reader(['en', 'ch_sim'])

# Japanese
reader = easyocr.Reader(['ja', 'en'])

# Multiple Latin-based languages
reader = easyocr.Reader(['en', 'fr', 'de', 'es'])
```

Full language list: https://www.jaided.ai/easyocr
# easyOCR
