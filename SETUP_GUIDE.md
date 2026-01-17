# CureBot - Setup & User Input Guide

## 📋 What User Needs to Provide

### 1. **Environment Variables (.env file)**
Create a `.env` file in the `hf-curebot/` folder with:

```env
# Google OAuth - for user authentication (OPTIONAL)
GOOGLE_CLIENT_ID=your_base64_encoded_google_client_id

# Google Maps API - for pharmacy location (OPTIONAL, uses OpenStreetMap by default)
GOOGLE_MAPS_API_KEY=your_google_maps_api_key

# Google Gemini API - for AI health advice (OPTIONAL but recommended)
GEMINI_API_KEY=your_base64_encoded_gemini_api_key
```

**How to get these:**
- **Google Client ID**: https://console.cloud.google.com/
- **Gemini API Key**: https://aistudio.google.com/ (Free!)
- **Google Maps API**: https://cloud.google.com/maps-platform

### 2. **Data Files**
Place these CSV files in `hf-curebot/` folder:
- `all_medicine databased.csv` - Medicine database (248K+ medicines) ✅
- `medicine_dataset.csv` - Medicine inventory (50K+ items) ✅

**Status**: Both files already included in the project

### 3. **Python Environment**
```bash
# Install dependencies
pip install -r requirements.txt

# Run the app
python web.py
```

---

## 🗑️ Unused Technologies Removed from web.py

### **Removed Imports:**
| Import | Reason | Used? |
|--------|--------|-------|
| `sklearn.preprocessing.normalize` | Not used in code | ❌ |
| `re` (regex module) | Not used in code | ❌ |
| `hashlib` | Not used in code | ❌ |
| `plotly.express as px` | Only `go` (graph_objects) is used | ❌ |
| `urllib.parse` | Not used in code | ❌ |

### **Still in use:**
- ✅ `dash` - Main web framework
- ✅ `pandas` - Data processing
- ✅ `numpy` - Numerical operations
- ✅ `sklearn.TfidfVectorizer` - Text vectorization (ML core)
- ✅ `sklearn.cosine_similarity` - Distance metrics (ML core)
- ✅ `difflib` - Medicine name matching
- ✅ `zipfile` - Extract medicine datasets
- ✅ `json` - API requests (Gemini)
- ✅ `base64` - API key encoding
- ✅ `datetime` - Timestamps
- ✅ `plotly.graph_objects` - Interactive charts
- ✅ `urllib.request` - HTTP requests for Gemini API
- ✅ `sentence_transformers` - Semantic search (ML core)

---

## 🎯 Main Project Files

### **Primary Entry Point**
```
hf-curebot/
├── web.py ⭐ MAIN FILE (Web UI + Full Application)
├── medimatch_app.py (ML Backend Core)
├── medimatch_ml.py (Alternative ML version)
└── requirements.txt (Dependencies)
```

### **File Descriptions**

#### **1. web.py** ⭐ Main Application File
- **What**: Complete web application with UI
- **Size**: ~3,370 lines
- **Tech**: Dash + Plotly + ML algorithms
- **Features**:
  - Web interface (HTML/CSS)
  - Chat bot interface
  - Medical query handling
  - Disease analytics with interactive graphs
  - Emergency mode with hospital finder
  - Pharmacy locator (OpenStreetMap)
  - Google Gemini AI integration
  - TF-IDF + Semantic search

**To run**: `python web.py`

#### **2. medimatch_app.py** - ML Backend
- **What**: Pure ML engine without UI
- **Size**: ~642 lines
- **Tech**: scikit-learn + Sentence Transformers
- **Features**:
  - TF-IDF vectorization
  - Semantic search (sentence embeddings)
  - Hybrid search algorithm
  - Data loading & preprocessing
  - Disease statistics
  - Gemini API integration

**Usage**: Imported by web.py for ML operations

#### **3. medimatch_ml.py** - Alternative ML Version
- Similar to medimatch_app.py
- Alternative implementation

---

## 📊 Architecture Overview

```
User Input
    ↓
web.py (Web Interface)
    ↓
├─→ TF-IDF Search (sklearn)
├─→ Semantic Search (Sentence Transformers)
└─→ Disease Analytics
    ↓
medimatch_app.py (ML Engine)
    ↓
├─→ Load CSV data
├─→ Train TF-IDF model
├─→ Create embeddings
└─→ Hybrid search
    ↓
Database (CSV files)
├─→ all_medicine databased.csv
└─→ medicine_dataset.csv
```

---

## 🔐 Security Notes

✅ **API Keys are now encoded:**
- Uses base64 encoding for sensitive keys
- Loaded from environment variables (`.env`)
- Never committed to git
- Add `.env` to `.gitignore`

✅ **Example .env file is provided:**
- `.env.example` shows required format
- User must create own `.env` file

---

## 🚀 Quick Start

1. **Clone/Download project**
2. **Create `.env` file** (copy from `.env.example`)
3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
4. **Run application**:
   ```bash
   python web.py
   ```
5. **Open browser**: `http://localhost:7860`

---

## 📦 Tech Stack Summary

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | Dash + Plotly | Web UI & Charts |
| **ML Core** | scikit-learn (TF-IDF) | Text vectorization |
| **Semantic** | Sentence Transformers | Advanced search |
| **Data** | pandas + numpy | Data processing |
| **API** | Google Gemini | AI health advice |
| **Maps** | Leaflet.js + OpenStreetMap | Pharmacy locator |

---

## ✅ Git Status

- ✅ Code pushed to HuggingFace Spaces
- ✅ All commits synchronized
- ✅ `.env.example` included for setup guide
- ❌ Cannot push to GitHub (authentication needed)

**To push to GitHub:**
```bash
git push github main  # Requires proper authentication
```

---

**Last Updated**: January 8, 2026  
**Version**: 3.0  
**Author**: CureBot Development Team
