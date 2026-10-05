# demo-app

A deliberately small FastAPI service used to learn CI/CD. The app is boring on
purpose -- the pipeline is the lesson.

## Endpoints

| Route | Purpose |
|---|---|
| `GET /` | service identity |
| `GET /health` | liveness/readiness -- used by the pipeline, proxy and monitors |
| `GET /version` | the running commit SHA -- your deploy receipt |
| `POST /sum` | real behaviour worth testing |

## Local setup

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements-dev.txt
pytest -q          # 10 passed
ruff check .       # All checks passed!
uvicorn app.main:app --reload
```

## Verify a deploy

```bash
curl -s http://<vm-ip>/version      # compare to: git rev-parse --short HEAD
```
