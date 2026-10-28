# Verification — 28 October 2026

| Checklist item | Evidence |
| --- | --- |
| Kaggle ML case study | `data/Iris.csv` downloaded directly from Kaggle's `uciml/iris` API; checksum in training provenance |
| Train/test using Jupyter | Executed `notebooks/01_iris_training.ipynb` through nbconvert and an IPython kernel, outside VS Code |
| Save model and parameters | `models/model.joblib` bundle and `models/parameters.json`; reload reproduces test predictions |
| FastAPI prediction | Five unittest groups pass; native real-HTTP smoke test passes on port 8019; project opened in VS Code |
| Docker endpoints | Local Compose container healthy on `127.0.0.1:8018`; real-HTTP health, metadata, OpenAPI, prediction and HTTP 422 rejection passed; responses saved in `docker-smoke.json` |
| New GitHub repository | https://github.com/24f2003970/iris-kaggle-mlops |
| GitHub Actions pipeline | `.github/workflows/ci.yml` committed and triggered by push |
| Successful pipeline | [Run 40639931517](https://github.com/24f2003970/iris-kaggle-mlops/actions/runs/40639931517) completed successfully for commit `84559118bc39cedea481e998736999760dc5c8dd`; every step passed, including Docker endpoint execution and evidence artifact upload |

The first CI run passed dependency installation, both API test stages, Jupyter execution and image build. Its HTTP probe encountered a transient connection reset before the container was ready. Readiness polling now retries connection resets and early HTTP disconnects as well as refused connections.

Measured held-out accuracy: **27/30 = 90%**; macro F1 **0.899749**. Small educational evaluation only.

Tests were executed through Python and HTTP tools; VS Code was opened for the API project. No claim is made that the tests were launched from VS Code's integrated terminal.
