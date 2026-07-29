# Titanic Survival Prediction

Two-part deploy on Render, same structure as the reference project:
- **Backend**: FastAPI (`main.py`) → Render "Web Service"
- **Frontend**: `index.html` + `style.css` + `script.js` → Render "Static Site"

## Folder structure
```
titanic_api/
├── main.py                      # FastAPI backend
├── requirements.txt             # dependencies
├── titanic_logistic_model.pkl   # your trained model (add this yourself)
├── index.html                   # frontend page
├── style.css
└── script.js
```

## Before deploying

Add your saved model file to this folder:
```
titanic_logistic_model.pkl
```
(created in your notebook with `joblib.dump(model, "titanic_logistic_model.pkl")`)

## Run locally

```
pip install -r requirements.txt
uvicorn main:app --reload
```

Backend: http://127.0.0.1:8000/docs
Frontend: just open index.html in your browser

## Deploy — Step 1: GitHub

Push this whole `titanic_api` folder to a GitHub repo.

## Deploy — Step 2: Backend on Render

1. Render → New → Web Service → connect your repo
2. Settings:
   - **Runtime**: Python 3
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `uvicorn main:app --host 0.0.0.0 --port $PORT`
3. Deploy — you'll get a URL like `https://titanic-api.onrender.com`

## Deploy — Step 3: Frontend on Render

1. Render → New → Static Site → connect the same repo
2. Settings:
   - **Build Command**: (leave blank)
   - **Publish Directory**: `.` (root, since index.html is at the top level)
3. Before/after deploying, open `script.js` and change `API_URL` to your live
   backend URL from Step 2, e.g.:
   ```
   const API_URL = "https://titanic-api.onrender.com/predict";
   ```
   Commit and push that change so the Static Site picks it up.

## Test

- Backend health check: `https://titanic-api.onrender.com/`
- Backend docs: `https://titanic-api.onrender.com/docs`
- Frontend: your Static Site URL, e.g. `https://titanic-frontend.onrender.com`
# titanic_1912
