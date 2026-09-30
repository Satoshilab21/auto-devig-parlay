# Image-to-devig showcase

A small Streamlit page for the saved example in `laya-lookup-testing.ipynb`.
It opens with the boosted parlay image, identifies the local Ollama model
(`gemma4:12b`), and shows its saved structured JSON output. Below that are
the Laya market and event choices and a devig preview using paired Pinnacle
odds captured in the notebook.

Run it with:

```powershell
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

For the notebooks, copy `.env.example` to `.env` and set `OLLAMA_HOST` to your
Ollama URL and `ODDS_SERVICE_TOKEN` to your odds-service token. The notebooks
read `OLLAMA_HOST` when calling `/api/chat`; `.env` is ignored by Git.

The page is a static showcase. It makes no Ollama, Laya, or odds-service calls.
The notebook fetches odds but does not calculate EV. The page's devig preview
normalizes each saved two-sided moneyline and multiplies the leg probabilities,
assuming independent games. The saved event choices and historical prices need
verification before use.
