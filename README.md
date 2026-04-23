# 🔍 Visual Search Engine

🚀 **Live Demo (Google Colab):**
👉 https://colab.research.google.com/drive/1QCLAEF38nqEe7cdpZuX8OVcOsuYLlwjA?usp=sharing

---

## 📌 Overview

This project is a **Visual Search Engine** that retrieves visually similar images from a dataset using deep learning and efficient similarity search.

Instead of relying on text-based search, the system understands **image content** through feature embeddings and returns the closest matches.

---

## 🖼️ Demo & Results

> Add your output screenshots / result images here

```
![Demo Image 1](path/to/image1.png)
![Demo Image 2](path/to/image2.png)
```

---

## ⚙️ Tech Stack

* **PyTorch** – Model handling and feature extraction
* **ResNet50** – Pretrained CNN for image embeddings
* **FAISS** – Fast similarity search (Facebook AI Similarity Search)
* **Google Colab** – Development & experimentation

---

## 🧠 How It Works

### 1. Offline Pipeline (Dataset Processing & Indexing)

**Flow:**

Dataset Images
→ Image Transformations (resize, normalize)
→ Feature Extraction (ResNet50)
→ Embedding Normalization
→ Store in FAISS Index

**Explanation:**

Each image in the dataset is passed through a pretrained ResNet50 model to extract feature embeddings.
These embeddings are normalized to make cosine similarity effective.
All embeddings are stored in a FAISS index for fast nearest-neighbor search.

---

### 2. Online Pipeline (User Query Search)

**Flow:**

User Input Image
→ Image Transformations
→ Feature Extraction (ResNet50)
→ Embedding Normalization
→ Cosine Similarity Search (FAISS)
→ Retrieve Top-K Similar Images

**Explanation:**

The query image goes through the same preprocessing and embedding steps.
FAISS compares this query embedding with stored dataset embeddings using cosine similarity.
The system returns the **Top-K most similar images**.

---

### 🔑 Key Idea

> Same embedding space + fast similarity search = efficient visual retrieval

---

## 🔧 Transformations & Normalization

### Transformations Applied

* Resize: (224, 224)
* Convert to Tensor
* Normalize using ImageNet statistics:

  * mean = [0.485, 0.456, 0.406]
  * std  = [0.229, 0.224, 0.225]

```python
transform = transforms.Compose([
    transforms.Resize((224,224)),
    transforms.ToTensor(),
    transforms.Normalize(
        [0.485,0.456,0.406],
        [0.229,0.224,0.225]
    )
])
```

### Why These Transformations?

* Matches input size expected by ResNet50
* Uses ImageNet normalization (same distribution as pretrained model)
* Improves feature extraction quality

---

## 📐 Embedding Normalization

```python
faiss.normalize_L2(embeddings)
```

### Why Normalize?

* Converts vectors to unit length
* Makes cosine similarity equivalent to inner product
* Improves retrieval accuracy and stability

---

## 💡 Additional Insight

- Embedding size: **2048**
- Each embedding is stored as a float32 vector → 4 bytes per dimension
- Memory per image ≈ 2048 × 4 = **8 KB**

📦 Storage in FAISS:
- Total storage grows linearly with dataset size
- Example:
  - 1K images → ~8 MB
  - 10K images → ~80 MB
  - 100K images → ~800 MB
---



## 🚀 Future Improvements

* Web-based interface (Streamlit / React)
* Hybrid search (text + image)
* Vision Transformers (CLIP)

---

## ▶️ How to Run

1. Clone this repository or open the provided Google Colab notebook
2. Add your Kaggle credentials
3. Run all cells

---

⭐ **If you like this project, don’t forget to star the repo!**
