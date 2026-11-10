# MovieRecommendation

MovieRecommendation is a recommendation engine for movies built on the [MovieLens](https://grouplens.org/datasets/movielens/) dataset. It takes a movie title as input and returns the movies in the dataset that are most similar to it. The notebook compares two approaches, collaborative filtering and content-based filtering, and evaluates them against a most-popular baseline.

![image](https://github.com/user-attachments/assets/9bdb8640-57cd-42ab-b4dd-4c506c538187)

> **Attribution:** [Confirm and add link: Steps 1-6 of the notebook are adapted from a publicly available MovieLens recommender tutorial.] The customized visualizations, the evaluation in Step 7, and the business proposal are our own additions.

## Tools

Python, with the following libraries:

- Pandas
- NumPy
- SciPy
- Scikit-learn
- Matplotlib
- Seaborn
- FuzzyWuzzy

## Data

The engine uses the `ml-latest-small` [MovieLens dataset](https://grouplens.org/datasets/movielens/): 100,836 ratings of 9,742 movies by 610 users. Only two files from the download are used:

- `ratings.csv`
- `movies.csv`

Download `ml-latest-small.zip`, unzip it, and place the `ml-latest-small` folder in the root of this repo. The data files are not included in the repo. If the folder is missing, the notebook falls back to a hosted copy of the same two files.

The notebook starts with exploratory analysis of the ratings and genres to understand the data before modeling.

![image](https://github.com/user-attachments/assets/4be51bf9-75c0-4ec3-92c3-a3ef51dbec56)

## Models

### Collaborative filtering

The first approach uses **k-Nearest Neighbors** (cosine similarity) on a user-movie utility matrix built from the ratings. It ignores all movie attributes and rests on one idea: movies rated similarly by the same users are similar to each other. Its main weakness is the **cold-start problem**: movies and users with few ratings get poor or no recommendations. The utility matrix here is about 98% empty (1.7% density).

### Content-based filtering

The second approach uses **cosine similarity** on a binary genre matrix. It does not need ratings, so it can score movies that collaborative filtering cannot, but genres alone are a coarse signal and many movies look identical to it.

### Supporting steps

- Movie titles are mapped to movie IDs so results are readable, because the models take and return IDs.
- `fuzzywuzzy` matches a misspelled title to the closest title in the dataset, so `juminji` still finds `Jumanji (1995)`.

## Evaluation

The notebook evaluates both approaches with an **offline, time-based holdout**:

- Each user's earliest 80% of ratings are used for training and their most recent 20% are held out for testing.
- A held-out movie counts as relevant if the user rated it 4.0 or higher.
- Candidate movies are scored by their similarity to the movies the user rated 4.0 or higher in the training period. Movies the user already rated are excluded.
- Both approaches are compared with a **most-popular baseline**, using precision@10, recall@10, hit rate@10, NDCG@10, and catalog coverage.

### Results

| Approach | Precision@10 | Recall@10 | Hit rate@10 | NDCG@10 | Coverage |
|---|---|---|---|---|---|
| Most popular (baseline) | [fill in] | [fill in] | [fill in] | [fill in] | [fill in] |
| Collaborative filtering (item-item kNN) | [fill in] | [fill in] | [fill in] | [fill in] | [fill in] |
| Content-based (genres) | [fill in] | [fill in] | [fill in] | [fill in] | [fill in] |

*Copy these from the output of Step 7 after running the notebook.*

### Limitations

- This is an offline evaluation. It measures agreement with past ratings, not whether users would enjoy or click the recommendations. Validating that would need an online test such as an A/B test.
- Results depend on the choices above (K = 10, the 4.0 threshold, the 80/20 time split) and come from a small dataset of 610 users, so differences between approaches should be read as indicative, not exact.
- Content-based filtering uses only 20 genre flags, so many movies are indistinguishable to it. Ties are broken by popularity.

## Files

- `Movie_Recommendation_System.ipynb`: the engine's code, exploratory analysis, and evaluation
- `Final Business Proposal.pptx`: our business proposal
- `Presentation.pdf`: a presentation of our solution, including the business problem it addresses
- `requirements.txt`: Python dependencies

## How to run

```
pip install -r requirements.txt
jupyter notebook Movie_Recommendation_System.ipynb
```

Then run all cells from top to bottom.

## Contributors

[Add team members and what each person worked on.]
