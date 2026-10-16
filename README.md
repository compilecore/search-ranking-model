# Search Ranking Engine

## Overview
A scientific document search and ranking system built using the SciFact
dataset. The system retrieves relevant research documents for a user query
and ranks them using BM25 and machine-learning models.

## Dataset
- Dataset: SciFact (BEIR benchmark)
- Corpus: 5,183 scientific documents
- Queries: 1,109
- Test relevance judgments: 339
- Unique test queries: 300

The dataset contains scientific claims, research documents, and relevance
judgments used to evaluate information retrieval systems.

## Models
- BM25: lexical information-retrieval baseline
- Logistic Regression: binary relevance classification
- Linear SVM: binary relevance classification
- Random Forest: relevance classification and reranking
- XGBoost: relevance classification
- Tuned Random Forest: Random Forest selected through grouped
  cross-validation and hyperparameter tuning

## Features
The machine-learning models use five features:
1. BM25 retrieval score
2. Query-term overlap
3. Query-term coverage
4. Document length
5. Query-term overlap with the document title

## End-to-End Test Results

| Model | MRR@10 | NDCG@10 |
|---|---:|---:|
| BM25 | 0.6186 | 0.6519 |
| Tuned Random Forest | 0.5814 | 0.6089 |

BM25 achieved higher scores than the tuned Random Forest in the current
end-to-end evaluation. The Random Forest reranker therefore requires
further improvement before it can be considered better than the baseline.

Evaluation uses the top 50 documents retrieved by BM25, followed by
ranking the candidates. These results do not evaluate alternative
retrieval methods or documents outside that candidate set.

## Project Structure

search_ranking_project/
├── search_ranking.ipynb
├── saved_models/
│   ├── search_ranking_models.pkl
│   ├── tuned_random_forest.pkl
│   └── xgboost_model.json
└── results/
    ├── ranking_results.json
    ├── end_to_end_results.json
    ├── final_test_comparison.png
    └── end_to_end_comparison.png

## How to Run
1. Open this project folder in VS Code.
2. Open the Jupyter notebook.
3. Select the Python environment containing the required libraries.
4. Run the notebook cells in order to load the dataset, build the index,
   train or load models, evaluate ranking performance, and run searches.
5. Use the interactive search cell to enter a scientific query and view
   the ranked documents.

The dataset path in the notebook may need to be updated to match your
computer.

## Evaluation Metrics
- MRR@10: measures how highly the first relevant result appears.
- NDCG@10: measures the quality of the ordering of relevant results
  within the top 10.

## Future Improvements
- Improve relevance ranking using learning-to-rank methods.
- Investigate queries for which BM25 retrieves weak candidates.
- Add a user interface for search and document inspection.
- Evaluate additional retrieval methods and compare their performance.
