# SixBatt — Grid Congestion Mitigation Dashboard

A Flask-based dashboard that uses [GridSFM](https://github.com/microsoft/GridSFM) (Microsoft's neural surrogate for AC Optimal Power Flow) to detect and mitigate power grid congestion through battery dispatch.

## How it works

The dashboard replicates the analysis flow: baseline OPF prediction → battery shutdown + re-prediction → mitigation report, visualised in-browser.

## Setup

**Requirements:** Python 3.10+

```bash
cd GridSFM/model
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -e .
pip install flask matplotlib networkx
```

### Download the model checkpoint

```bash
# Option A — via Hugging Face CLI
hf download microsoft/GridSFM_Open gridsfm_open_v1.1.pt --local-dir checkpoints

# Option B — from Python
python -c "from gridsfm import load_from_hf; load_from_hf('microsoft/GridSFM_Open')"
```

## Run the dashboard

```bash
cd GridSFM/model
python dashboard.py
```

Then open **http://localhost:5050** in your browser.

The first request loads the model (may take a few seconds on CPU); subsequent requests are faster.
