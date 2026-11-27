# 🎬 TMDB Movie Recommendation System

This repository provides a complete End-to-End AI/ML Movie Recommendation System built on top of the classic **TMDB 5000 Movie Dataset**.

## 🛠️ Technologies Used
* **Python 3.10+**
* **Pandas / NumPy** (Data wrangling & matrices)
* **Scikit-Learn** (TF-IDF vectorizer & cosine distance maps)
* **Matplotlib / Seaborn** (Data exploration)
* **Gradio** (Modern Web UI interface)

## 🚀 Project Steps
1. **Data Integration**: Joined raw metadata features safely.
2. **Feature Extraction**: Evaluated nested JSON items safely using `ast.literal_eval` to fetch cast, keywords, genres, and directors.
3. **Metadata Combination**: Created a metadata-soup feature vector `combined_features`.
4. **Scalable Cosine-Similarity Engine**: Implemented an on-demand, memory-efficient algorithm to dynamically compute similarity arrays.
5. **IMDb Weighted Scoring Formula**: Implemented a popularity-based engine to suggest high-performing global favorites.
6. **Hybrid System**: Unified text features and weighted performance indices smoothly.

## 📊 Dataset Description
This project utilizes the **TMDB 5000 Movie Dataset**, which consists of two interconnected tables:
* **tmdb_5000_movies.csv**: Contains metadata for 4,803 films (including columns such as budget, genres, homepage, id, keywords, original_language, original_title, overview, popularity, release_date, revenue, runtime, vote_average, and vote_count).
* **tmdb_5000_credits.csv**: Contains details on film talent, specifically the structured string records for `cast` and `crew` lists linked by `movie_id`.

## 🔑 Key Features
* **Robust JSON Handling**: Custom parsers safely handle stringified nested data fields using `ast.literal_eval`.
* **Metadata Cleaning**: Extracted and normalized genres, keywords, cast, director, overview and language while preserving spaces between words.
* **Content-Based Recommendations**: Uses TF-IDF and cosine similarity to find movies with similar metadata.
* **IMDb-Style Weighted Rating**: Balances movie ratings with vote counts to reduce the influence of movies with very few votes.
* **Hybrid Recommendations**: Combines 60% content similarity and 40% normalized weighted popularity.
* **Interactive Interface**: Gradio-based interface for selecting movies and recommendation modes.

## 🧮 Recommendation Algorithms

### A. Content-Based Filtering
Movie metadata is transformed into numerical vectors using Term Frequency-Inverse Document Frequency (TF-IDF), with a maximum of 10,000 features. Cosine similarity measures the similarity between two movie vectors:
$$\text{Cosine Similarity}(A,B)=\frac{A\cdot B}{\|A\|\|B\|}$$
The system calculates similarities on demand instead of storing a complete movie-to-movie similarity matrix.

### B. IMDb-Style Weighted Rating
The system uses the weighted rating formula:
$$WR=\frac{v}{v+m}R+\frac{m}{v+m}C$$
Where:
* **$v$**: Number of votes for a movie (`vote_count`)
* **$m$**: Minimum vote threshold (90th percentile of vote counts, approximately 1838.4)
* **$R$**: Movie's average rating (`vote_average`)
* **$C$**: Mean rating across the dataset (approximately 6.092)

### C. Hybrid Recommendation
The hybrid model combines content similarity and normalized weighted popularity:
$$\text{Hybrid Score}=0.6S+0.4P$$
Where:
* **$S$**: Content similarity score
* **$P$**: Normalized weighted popularity score

## 📈 Model Evaluation & Observations
The recommendation system was tested using multiple movies, including Avatar, The Dark Knight Rises, Spectre, Interstellar and The Avengers.
* **Content Similarity**: The Dark Knight Rises returned The Dark Knight with a similarity score of 0.4741.
* **Genre Jaccard Overlap**: The Dark Knight Rises achieved an average genre Jaccard overlap of 0.51 across its top five content-based recommendations.
* **Hybrid Recommendations**: For The Avengers, Avengers: Age of Ultron ranked first with a hybrid score of 0.5872.
* **Popularity Influence**: For Interstellar, The Empire Strikes Back ranked first with a hybrid score of 0.4145.

These are proxy evaluation observations. They do not represent measured user satisfaction or standard precision/recall metrics.

## ⚠️ Limitations
* **No User-Level Ratings**: The TMDB 5000 dataset does not contain individual user-movie rating interactions.
* **Collaborative Filtering**: A genuine collaborative filtering model has not been implemented.
* **Popularity Bias**: The hybrid model may recommend highly rated movies with relatively low content similarity because popularity contributes 40% of the hybrid score.
* **Cold Start**: New movies with limited metadata may receive weaker content-based recommendations.

## 🔮 Future Scope
* Integrate MovieLens ratings to implement collaborative filtering using matrix factorization or user/item-based methods.
* Explore transformer-based text embeddings such as Sentence-BERT.
* Improve hybrid score weighting through systematic evaluation.
* Add movie posters, descriptions and additional filtering options to the interface.

## 💻 Installation & Google Colab Execution
1. Open the project notebook in Google Colab.
2. Upload or mount the TMDB dataset files.
3. Run notebook cells sequentially, starting with dataset loading and preprocessing.
4. Install the required Python libraries if they are not already available.
5. Run the Gradio interface cell to launch the interactive application.

A standard CPU runtime is sufficient for this project; GPU is optional.

## 📦 Saved Artifacts
* **`recommendation_data.csv`**: Processed movie metadata containing extracted features and recommendation-related fields.
* **`tfidf_model.pkl`**: Pickled tuple containing the fitted TF-IDF vectorizer and its transformed sparse matrix.

## 📂 Project Folder Structure
```text
TMDB-Movie-Recommendation-System/
├── tmdb_dataset/
│   ├── tmdb_5000_movies.csv
│   └── tmdb_5000_credits.csv
├── recommendation_data.csv
├── tfidf_model.pkl
├── TMDB_Movie_Recommendation_System.ipynb
└── README.md
```

## 🖥️ Gradio Interface Instructions
1. Run the Gradio interface cell in Google Colab.
2. Open the temporary public URL generated in the output.
3. Enter a movie title, such as `Avatar` or `Spectre`.
4. Select a recommendation mode:
   - Pure Content Similarity
   - IMDb Weighted Rating Popularity
   - Hybrid
5. Choose the desired number of recommendations and submit.

The public Gradio share link is temporary and depends on the active runtime.
## 👥 17. Author

- **Your Name**
- GitHub: [Your GitHub Profile](https://github.com/your-username)
- LinkedIn: [Your LinkedIn Profile](https://www.linkedin.com/in/your-profile/)
