# Parlay Auto Devig

This repository showcases an automated workflow for evaluating boosted sports parlays. The full tool is designed to reduce a manual devig process that can take 3–5 minutes to under 20 seconds, depending on hardware and available odds data. The main showcase is the [notebook walkthrough](auto-devig-demo.ipynb), which includes the example bet slip, code, and saved outputs.

## How the tool works

1. A user sends a parlay screenshot to a Telegram bot.
2. A locally hosted Gemma 4 12B model receives the image through Ollama over Tailscale and extracts the legs into structured data.
3. The extracted details drive a broad search of the odds database.
4. A locally hosted Laya decision model narrows ambiguous results by identifying the market and matching the event.
5. The tool retrieves odds for both sides of each leg, calculates the parlay's expected value, and replies through Telegram.

The notebook walks through **one leg**, from image extraction to retrieving both sides of its odds. It does not run the Telegram bot or calculate the final expected value. The [example result image](auto-devig-examples/result-example.png) shows the full tool's Telegram response.

## Explore the notebook

Open [auto-devig-demo.ipynb](auto-devig-demo.ipynb) on GitHub to read the explanation and inspect its saved outputs. The walkthrough covers the extraction schema, odds search, Laya's market and event choices, and the final odds lookup.

To run it locally, install the notebook dependencies in your Python environment:

```powershell
python -m pip install -r requirements-dev.txt
```

Open the notebook in VS Code or another Jupyter-compatible editor. Create a `.env` file in the repository root with the connection settings used by the notebook:

```dotenv
OLLAMA_HOST=http://your-ollama-host:11434
ODDS_SERVICE_URL=https://your-odds-service
ODDS_SERVICE_TOKEN=your-token
```

Running the cells requires access to an Ollama server with `gemma4:12b`, the odds service, and Laya's model files. The notebook searches for current odds, so its historical example screenshot may no longer produce the saved lookup results when rerun. The `.env` file is ignored by Git.
