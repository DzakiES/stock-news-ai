# 📈 Stock News Sentiment Analysis - BBCA

> **Tugas Akhir - Telkom University**  
> Analisis Sentimen Berita Saham Bank Central Asia (BBCA) Menggunakan Large Language Models

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)
![AI](https://img.shields.io/badge/AI-LLM-green.svg)

---

## 📋 Deskripsi Proyek

Proyek ini mengimplementasikan sistem **analisis sentimen berita saham BBCA** secara otomatis menggunakan dua Large Language Model (LLM):

- **Google Gemini 2.5 Pro**
- **OpenAI GPT**

Sistem ini menggunakan teknik:

- **RAG (Retrieval-Augmented Generation)** dengan ChromaDB sebagai vector store
- **Chain of Thought (CoT)** untuk penalaran bertahap
- **Web Scraping** untuk mengambil berita dari CNBC Indonesia

---

## 🏗️ Arsitektur Sistem

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  Web Scraper    │────▶│  Vector Store    │────▶│   LLM Model     │
│  (CNBC News)    │     │   (ChromaDB)     │     │ (Gemini/OpenAI) │
└─────────────────┘     └──────────────────┘     └────────┬────────┘
                                                          │
                                                          ▼
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│ Recommendation  │◀────│ Sentiment Score  │◀────│   CoT Analysis  │
│   Buy/Hold/Sell │     │  POSITIF/NEGATIF │     │   (Reasoning)   │
└─────────────────┘     └──────────────────┘     └─────────────────┘
```

---

## 📁 Struktur File

```
stock-news-ai/
│
├── 📓 Notebooks
│   ├── Gemini_cnbc.ipynb         # Analisis sentimen dengan Google Gemini
│   ├── OpenAI_CNBC.ipynb         # Analisis sentimen dengan OpenAI GPT
│   └── Model_Evaluation.ipynb    # Evaluasi & perbandingan performa model
│
├── 📊 Hasil Analisis
│   ├── bbca_sentiment_report_gemini.json   # Output analisis Gemini
│   ├── bbca_sentiment_report_openai.json   # Output analisis OpenAI
│   └── evaluation_report_comprehensive.txt # Laporan evaluasi lengkap
│
├── 📈 Visualisasi
│   ├── confusion_matrix_comparison.png
│   ├── score_distribution_comparison.png
│   ├── comprehensive_evaluation_with_metrics.png
│   └── gemini_100_accuracy_analysis.png
│
└── 📄 README.md
```

---

## ⚙️ Instalasi & Setup

### 1. Clone Repository

```bash
git clone https://github.com/DzakiES/stock-news-ai.git
cd stock-news-ai
```

### 2. Install Dependencies

**Untuk Gemini:**

```bash
pip install google-generativeai chromadb beautifulsoup4 requests sentence-transformers lxml
```

**Untuk OpenAI:**

```bash
pip install openai chromadb beautifulsoup4 requests sentence-transformers lxml
```

**Untuk Evaluasi:**

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

### 3. Setup API Keys

**Gemini API:**

```python
GEMINI_API_KEY = "your-gemini-api-key"
```

Dapatkan API key di: [Google AI Studio](https://aistudio.google.com/)

**OpenAI API: (GPT-OSS-20P)**

```python
OPENAI_API_KEY = "your-openai-api-key"
```

## untuk API openai bisa menggunakan yang free jika masih tersedia

## 🚀 Cara Penggunaan

### 1. Analisis Sentimen dengan Gemini

```python
# Buka Gemini_cnbc.ipynb
analyzer = BBCANewsAnalyzer(gemini_api_key="YOUR_API_KEY")
analyzer.scrape_cnbc_news(search_url, max_articles=25, max_pages=5)
results = analyzer.analyze_all_articles()
```

### 2. Analisis Sentimen dengan OpenAI

```python
# Buka OpenAI_CNBC.ipynb
analyzer = BBCANewsAnalyzer(openai_api_key="YOUR_API_KEY")
analyzer.scrape_cnbc_news(search_url, max_articles=25, max_pages=5)
results = analyzer.analyze_all_articles()
```

### 3. Evaluasi & Perbandingan Model

```python
# Buka Model_Evaluation.ipynb
# Jalankan semua cell untuk melihat perbandingan performa
```

---

## 📊 Hasil Evaluasi

### Performa Model

| Model                | Accuracy | Precision | Recall | F1-Score |
| -------------------- | -------- | --------- | ------ | -------- |
| **Gemini 2.5 Flash** | 88.24%   | 77.78%    | 80.00% | 78.55%   |
| **OpenAI GPT**       | 88.24%   | 83.33%    | 80.00% | 81.58%   |

### Metrik Validasi

| Metode               | Hasil                               |
| -------------------- | ----------------------------------- |
| **Cohen's Kappa**    | 0.7069 (Substantial Agreement)      |
| **Agreement Rate**   | 82.4% artikel disetujui kedua model |
| **Bootstrap 95% CI** | [70.59% - 100.00%]                  |

### Kesimpulan

- ✅ Kedua model menunjukkan performa **SETARA** secara statistik (~88% accuracy)
- ✅ Cohen's Kappa 0.707 menunjukkan **substantial agreement** antar model
- ✅ OpenAI sedikit lebih unggul pada F1-Score (81.58% vs 78.55%)
- ✅ Gemini memiliki **confidence calibration** yang lebih baik (r = 0.6583)

---

## 🔧 Teknologi yang Digunakan

| Kategori            | Teknologi                                |
| ------------------- | ---------------------------------------- |
| **Language**        | Python 3.8+                              |
| **LLM**             | Google Gemini 2.5 Pro, OpenAI GPT        |
| **Vector Store**    | ChromaDB                                 |
| **Embedding**       | Sentence-Transformers (all-MiniLM-L6-v2) |
| **Web Scraping**    | BeautifulSoup4, Requests                 |
| **Data Processing** | Pandas, NumPy                            |
| **Visualization**   | Matplotlib, Seaborn                      |
| **ML Metrics**      | Scikit-learn                             |

---

## 📝 Fitur Utama

1. **Web Scraping Otomatis**

   - Scraping berita BBCA dari CNBC Indonesia
   - Pagination support untuk multiple pages
   - Ekstraksi judul, konten, dan tanggal

2. **RAG (Retrieval-Augmented Generation)**

   - Knowledge base indikator saham positif/negatif
   - Context retrieval dari ChromaDB
   - Enhanced prompt dengan konteks relevan

3. **Chain of Thought Analysis**

   - Analisis step-by-step
   - Reasoning yang transparan
   - Confidence score per prediksi

4. **Comprehensive Evaluation**
   - Multiple validation methods
   - Cohen's Kappa inter-rater agreement
   - Bootstrap confidence intervals
   - Confusion matrix visualization

---

## 📄 License

Proyek ini dibuat untuk keperluan akademik - Tugas Akhir Telkom University.

---

## 👤 Author

**[Nama Anda]**  
Teknik Informatika - Telkom University

---

## 🙏 Acknowledgments

- Google AI untuk Gemini API
- OpenAI untuk GPT API
- CNBC Indonesia sebagai sumber data berita
