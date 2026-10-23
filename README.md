<div align="center">
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:06283d,35:1363df,70:47b5ff,100:dff6ff&height=190&section=header&text=HYDRA&fontSize=68&fontColor=ffffff&animation=twinkling&fontAlignY=36&desc=Read%20water%20from%20space.&descAlignY=58&descSize=18" alt="HYDRA animated header" />

  <a href="https://readme-typing-svg.demolab.com"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=18&pause=1100&color=47B5FF&center=true&vCenter=true&width=720&lines=Choose+a+water+body;Load+HLS+granules;Inspect+the+map+and+index" alt="Typing tagline" /></a>

  <p>
    <img src="https://img.shields.io/badge/Python-3.11%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
    <img src="https://img.shields.io/badge/Streamlit-dashboard-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white" alt="Streamlit" />
    <img src="https://img.shields.io/badge/Data-HLS%20%2B%20NASA%20CMR-1363DF?style=for-the-badge" alt="HLS and NASA CMR" />
    <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-DFF6FF?style=for-the-badge" alt="MIT License" /></a>
  </p>
</div>

## 🌊 What it does

H.Y.D.R.A. is a Streamlit prototype for exploring satellite imagery over selected water regions. It queries NASA's CMR for Harmonized Landsat-Sentinel granules, processes imagery, and presents map-based analysis with saved presets and analysis history.

<p align="center">
  <img src="https://raw.githubusercontent.com/ChristopherJoshy/hydra/main/Tampa%20Bay%20(Florida).png" width="48%" alt="HYDRA Tampa Bay analysis map" />
  <img src="https://raw.githubusercontent.com/ChristopherJoshy/hydra/main/Lake%20Erie%20(USA).png" width="48%" alt="HYDRA Lake Erie analysis map" />
</p>

## 🛰️ Processing path

```mermaid
flowchart LR
  A[Region and date range] --> B[NASA CMR granules]
  B --> C[Download and cache imagery]
  C --> D[Cloud mask and band processing]
  D --> E[Normalized single-band index]
  E --> F[Map and severity view]
  F --> G[SQLite history and presets]
```

## 🧪 Important measurement note

The current code calls its value `NDCI`, but computes a normalized single-band brightness index from the available composite. It is **not the standard red/red-edge NDCI formula**. The thresholds are prototype heuristics, not a validated environmental or public-health measurement. Treat the map as an exploratory visualization, not a confirmed bloom report.

## 🧰 Stack

| Area | Tools |
|---|---|
| Interface | Python, Streamlit, streamlit-folium, Folium |
| Imagery | NASA CMR, HLS, GIBS; Rasterio, NumPy, Pillow |
| Processing | Pandas, Matplotlib, Requests |
| Local state | SQLite, filesystem cache |

## 🚀 Run locally

```bash
git clone https://github.com/ChristopherJoshy/hydra.git
cd hydra
python -m venv .venv
# Windows: .venv\Scripts\Activate.ps1
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
streamlit run main.py
```

NASA Earthdata credentials may be needed to download source granules. Copy `.env.example` to `.env` and set credentials locally, or export them in the shell. Never commit the `.env` file.

## 🧪 Tests

```bash
pytest
```

## 🗂️ Layout

```text
main.py          Streamlit interface, CMR requests, processing and SQLite state
evaluate.py      analysis/evaluation helper
*.png            saved map views used as README examples
tests/           project tests
```

## 📄 License

MIT. See [`LICENSE`](LICENSE).