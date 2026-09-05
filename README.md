# 🎬 Movie Recommendation System

A content-based movie recommendation system that uses **TF-IDF vectorization** and **cosine similarity** to recommend movies based on their metadata. The project combines a **FastAPI backend**, **Streamlit frontend**, and **TMDB API** to provide movie search, details, posters, and personalized recommendations. 

## ✨ Features

* **Content-Based Recommendations** using TF-IDF and cosine similarity.
* **Genre-Based Recommendations** using TMDB movie genres.
* **Movie Search** with TMDB integration.
* **Movie Details** including title, overview, release date, genres, posters, and ratings.
* **Hybrid Recommendations** combining local TF-IDF recommendations with TMDB genre recommendations.
* **Interactive Streamlit UI** with autocomplete search and movie grids.
* **REST API** built with FastAPI and Pydantic response models.
* **Asynchronous TMDB API calls** using `httpx`.
* **Cached API responses** in Streamlit for faster interactions.
* **Health Check Endpoint** for backend monitoring. 

## 🏗️ Architecture

```text
                    ┌─────────────────────┐
                    │    Streamlit UI     │
                    │   Search & Display   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │    FastAPI Backend  │
                    │                     │
                    │  REST API Endpoints│
                    └───────┬───────┬─────┘
                            │       │
                  ┌─────────┘       └──────────┐
                  ▼                            ▼
        ┌──────────────────┐         ┌─────────────────┐
        │ Local ML Pipeline│         │    TMDB API     │
        │                  │         │                 │
        │ TF-IDF Matrix    │         │ Search          │
        │ Cosine Similarity│         │ Movie Details   │
        │ Movie Metadata   │         │ Genre Discovery │
        └──────────────────┘         └─────────────────┘
```

## 🧠 Recommendation Approach

The recommendation engine uses a **content-based filtering** approach.

1. Movie metadata is processed and stored locally.
2. Text features are transformed using **TF-IDF vectorization**.
3. Movie representations are compared using **cosine similarity**.
4. The most similar movies are ranked and returned as recommendations.
5. TMDB is queried to enrich recommendations with posters, release dates, ratings, and other metadata. 

The repository stores the precomputed dataframe, title-index mapping, TF-IDF vectorizer, and TF-IDF matrix as serialized files for runtime retrieval. ([GitHub][1])

## 🔌 API Endpoints

| Endpoint                  | Description                                                            |
| ------------------------- | ---------------------------------------------------------------------- |
| `GET /health`             | Check API health                                                       |
| `GET /home`               | Retrieve popular, trending, top-rated, upcoming, or now-playing movies |
| `GET /tmdb/search`        | Search movies through TMDB                                             |
| `GET /movie/id/{tmdb_id}` | Fetch movie details                                                    |
| `GET /recommend/genre`    | Get genre-based recommendations                                        |
| `GET /recommend/tfidf`    | Get TF-IDF similarity recommendations                                  |
| `GET /movie/search`       | Get movie details + TF-IDF + genre recommendations                     |

The backend defines these routes using FastAPI and validates response structures with Pydantic models. 

## 🛠️ Tech Stack

* **Language:** Python
* **Machine Learning:** Scikit-learn
* **Data Processing:** Pandas, NumPy
* **Similarity Search:** TF-IDF, Cosine Similarity, SciPy
* **Backend:** FastAPI, Uvicorn
* **Frontend:** Streamlit
* **External API:** TMDB API
* **HTTP:** HTTPX, Requests
* **Validation:** Pydantic

The repository's dependency file confirms the core Python packages and versions used by the application. 

## 📁 Project Structure

```text
movie-rec/
│
├── app.py                  # Streamlit frontend
├── main.py                 # FastAPI backend
├── movies.ipynb            # Data processing / recommendation development
├── movies_metadata.csv     # Movie metadata
│
├── df.pkl                  # Processed movie dataframe
├── indices.pkl             # Movie title → index mapping
├── tfidf.pkl               # TF-IDF vectorizer
├── tfidf_matrix.pkl        # Precomputed TF-IDF matrix
│
├── requirements.txt        # Python dependencies
├── runtime.txt             # Runtime configuration
└── .gitignore
```

The repository contains the Streamlit app, FastAPI service, notebook, movie dataset, and precomputed recommendation artifacts. ([GitHub][1])

## 🚀 Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/master-temp/movie-rec.git
cd movie-rec
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it:

**Windows**

```bash
venv\Scripts\activate
```

**Linux/macOS**

```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure TMDB API

Create a `.env` file:

```env
TMDB_API_KEY=your_tmdb_api_key
```

The FastAPI application loads the API key from the environment and raises an error if it is not configured. 

### 5. Start FastAPI

```bash
uvicorn main:app --reload
```

The API will be available at:

```text
http://127.0.0.1:8000
```

### 6. Start Streamlit

In another terminal:

```bash
streamlit run app.py
```

## 🌐 Deployment

The Streamlit application is configured to communicate with a deployed FastAPI backend, and the project is designed for an end-to-end web deployment architecture. 

## 📊 Recommendation Example

For a selected movie:

```text
Movie
  ↓
TMDB Search
  ↓
Movie Details
  ↓
┌─────────────────────┬─────────────────────┐
│ TF-IDF Similarity   │ Genre Recommendations│
│                     │                     │
│ Similar Movies      │ Popular Movies      │
└─────────────────────┴─────────────────────┘
```

## 🔮 Future Improvements

* Add collaborative filtering using user-rating data.
* Combine content and collaborative filtering into a hybrid recommendation model.
* Add model evaluation metrics such as Precision@K and Recall@K.
* Improve ranking using weighted metadata and user preferences.
* Add authentication and personalized user profiles.

## 📄 License

Add your preferred license here, such as **MIT License**, if you intend to publish the repository under an open-source license.

---

**GitHub Description**

> Content-based movie recommendation system using TF-IDF, cosine similarity, FastAPI, Streamlit, and TMDB API.

[1]: https://github.com/master-temp/movie-rec "GitHub - master-temp/movie-rec · GitHub"
