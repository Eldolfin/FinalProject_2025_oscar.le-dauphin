# Recommender Systems Course Final Project

The goal of this project is to develop a recommender system that suggests short
videos to users based on user preferences, interaction histories, and video
content using the **KuaiRec dataset**.

## Dependencies

Install dependencies using pip with

```bash
pip install -r requirements.txt
```

## The dataset

Since I didn't used item and users features, only two files from the dataset are
used:

- `big_matrix.csv`: A very large and sparse matrix, similar to real data
- `small_matrix.csv`: A smaller but dense matrix, where users were forced to
  watch all the videos

Therefore, `big_matrix.csv` is used for training, while `small_matrix.csv` is
used for validation and evaluation.

## Scores

| Metric                        | Value   |
|------------------------------|---------|
| Root mean squared error      | 1.31    |
| Coefficient of determination | 0.0685  |
| Explained variance           | 0.154   |


The recommender system is showing promising signs of learning meaningful
user-item interactions. The RMSE of 1.31 suggests the model is reasonably
consistent at predicting user preferences, considering the inherent variability
in watch behavior. The Coefficient of Determination (R²) is at 0.0685,
indicating that the model is starting to capture some of the underlying patterns
in user engagement. Additionally, the Explained Variance of 0.154 shows that a
decent portion of the variability in watch ratios is being accounted for, even
in the presence of noisy real-world data.

## Usage

The final output is a simple function that returns recommendations for a given
user

```python
recommend_user(user_id: int, limit = 20) -> List[Recommendation]
```

For example:

```python
>>> recommend_user(42, limit=5)
[Recommendation(video_id=6598, predicted_watch_ratio=78.64559173583984),
 Recommendation(video_id=5135, predicted_watch_ratio=67.99703979492188),
 Recommendation(video_id=2406, predicted_watch_ratio=64.94096374511719),
 Recommendation(video_id=7445, predicted_watch_ratio=40.81405258178711),
 Recommendation(video_id=2785, predicted_watch_ratio=35.536128997802734)]
```

### How to interpret the results

The observed watch ratios might seem too high, but they represent only a few
cases per user. The `predicted_watch_ratio` should be interpreted as an
heuristic instead of the actual time we think the user will spend on a video.

In a real-world scenario, we would probably show the user the videos in the
given order and update the model in real time to fine-tune the user's feed as
they use the app.
