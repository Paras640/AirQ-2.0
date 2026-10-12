# AirQ 2.0

AirQ predicts short-term air quality using a Flask API and a React frontend. The API serves Random Forest model predictions and live AQI data for the frontend.

## Project structure

```text
.
|-- app.py                    Flask API entry point
|-- main.py, predict.py,
|   surroundings.py            Backend modules
|-- model_manager.py          Model loading and fallback generation
|-- aqi predictor.py          Model training script
|-- exports/                  Trained models and model metadata
|-- india_aqi_v6_2024-2025.csv
|-- AQI_Prediction_India_1.ipynb
|-- TEST/                     React + TypeScript + Vite frontend
|-- requirements.txt          Python dependencies
|-- Procfile                  Railway backend start command
|-- .railwayignore            Keeps the frontend out of Railway builds
`-- vercel.json               Vercel routing configuration
```

The frontend remains in `TEST/` to preserve the existing deployment configuration.

## Run locally

### Backend

Use Python 3.11.9, matching `.python-version`.

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python app.py
```

The API starts at `http://localhost:5000`.

### Frontend

In a second terminal:

```powershell
Set-Location TEST
npm install
npm run dev
```

The frontend uses `http://localhost:5000` for its API by default. Set `VITE_API_URL` before starting Vite to use a different backend URL.

## API endpoints

- `GET /health` - backend and model status
- `GET /live-aqi` - live AQI ticker data
- `POST /predict` - one-hour and 24-hour AQI predictions

## Frontend checks

Run from `TEST/`:

```powershell
npm run type-check
npm run lint
npm run build
```
