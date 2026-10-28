# Verification — 28 October 2026

| Checklist item | Evidence |
| --- | --- |
| Kaggle ML case study | `data/Iris.csv` downloaded directly from Kaggle's `uciml/iris` API; checksum in training provenance |
| Train/test using Jupyter | Executed `notebooks/01_iris_training.ipynb` through nbconvert and an IPython kernel, outside VS Code |
| Save model and parameters | `models/model.joblib` bundle and `models/parameters.json`; reload reproduces test predictions |
| FastAPI prediction | Five unittest groups pass; native real-HTTP smoke test passes on port 8019; project opened in VS Code |
| Docker endpoints | Pending final local smoke test; CI's initial Docker build passed |
| New GitHub repository | https://github.com/24f2003970/iris-kaggle-mlops |
| GitHub Actions pipeline | `.github/workflows/ci.yml` committed and triggered by push |
| Successful pipeline | Pending rerun after correcting startup readiness polling |

The first CI run passed dependency installation, both API test stages, Jupyter execution and image build. Its HTTP probe encountered a transient connection reset before the container was ready. Readiness polling now retries connection resets and early HTTP disconnects as well as refused connections.

Measured held-out accuracy: **27/30 = 90%**; macro F1 **0.899749**. Small educational evaluation only.

Tests were executed through Python and HTTP tools; VS Code was opened for the API project. No claim is made that the tests were launched from VS Code's integrated terminal.
