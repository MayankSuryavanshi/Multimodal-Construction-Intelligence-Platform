# Multimodal-Construction-Intelligence-Platform
## Skill Wallet Capstone Project 1

An AI-powered **Streamlit application** that brings site safety auditing, structural defect diagnostics, project valuation, and field assistance into one dashboard. It uses Google Gemini for multimodal analysis, runs with zero external database dependencies, and can be deployed to Streamlit Community Cloud.

> ⚠️ **Disclaimer:** All AI output is advisory. Safety-critical and structural decisions must be verified by a licensed engineer or qualified safety officer. Valuation figures are indicative estimates, not a certified valuation.

## ✨ Features

| **Tab** | **Epic** | **What it does** |
|---|---|---|
| 🦺 **Site Safety & PPE Audit** | Epic 2 | Upload a site photo. Gemini checks helmets, high-visibility vests, steel-toe boots, and safety harnesses, and identifies potential hazards using OSHA and IS 456 references. Returns a safety score (0–100), overall status, PPE checklist, hazards with severity (Low / Medium / High / Critical), corrective remedies, and a downloadable JSON report. |
| 🧱 **Crack Diagnostics** | Epic 2 | Upload a concrete or wall photo. Classifies defects (Hairline, Settlement, Structural Shear, Thermal Expansion, Spalling), estimates crack width in mm, and lists possible causes, repair options, urgency, and a monitoring plan. Includes a downloadable JSON report. |
| 💰 **Planning & Valuation** | Epic 3 | Choose structure type, built-up area in sq ft, location tier (1/2/3), and completion percentage. Estimates total budget, CapEx incurred, current asset valuation (₹ Lakhs / Crores), steel and cement requirements, and milestone progress. Generates a conceptual 3D render using Pollinations AI. |
| 🌦️ **Daily Site Assistant** | Epic 5 | Select weather conditions (High Wind, Heavy Rain, Extreme Heat, Normal) to receive dynamic safety alerts, such as crane suspension, electrical hazard mitigation, and concrete-curing guidance. Includes a multi-turn construction engineering chatbot. |

### Sidebar

- Masked Gemini API key input
- Model selector
- Live/demo status indicator
- Module navigation
- Architecture overview

**Demonstration mode:** If no API key is provided, or a Gemini request fails, the app falls back to sample output so each feature can still be explored.

## 🏛️ Architecture

```text
Streamlit UI (tabs)
   │
   ├── Image modules ──► Pillow ──► Gemini Vision (JSON mode)
   │                                  │
   │                                  └──► Schema normalizer
   │                                        └──► Metric cards / JSON export
   │
   ├── Valuation engine ──► Pure-Python cost model
   │                         └──► Pollinations render URL
   │
   └── Daily assistant ──► Gemini chat
                             └──► Weather-aware system context

State: st.session_state only
Database: None
```

## 🚀 Quick Start

### 1. Clone the repository

Replace `<your-username>` and `<your-repo>` with your GitHub username and repository name.

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

### 2. Create and activate a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the application

```bash
streamlit run app.py
```

### 5. Configure your Gemini API key

Get an API key from [Google AI Studio](https://aistudio.google.com/), then enter it in the app's sidebar.

Alternatively, create `.streamlit/secrets.toml` in your project:

```toml
GEMINI_API_KEY = "your-key-here"
```

Add `.streamlit/secrets.toml` to `.gitignore`. **Never commit API keys or secrets to GitHub.**

## ☁️ Deploy on Streamlit Community Cloud

1. Push your project repository to GitHub.
2. Open [Streamlit Community Cloud](https://share.streamlit.io/).
3. Click **New app** and select your repository and branch.
4. Set the main file path to `app.py`.
5. Under **Advanced settings → Secrets**, optionally add:

   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```

6. Click **Deploy**.

## 📁 Project Structure

```text
.
├── app.py                 # Streamlit application
├── requirements.txt       # Python dependencies
├── README.md              # Project documentation
├── .gitignore             # Files excluded from Git
└── .streamlit/
    └── secrets.toml       # Local secrets (do not commit)
```

## 🧮 Valuation Model (Tab 3)

| **Quantity** | **Formula / approach** |
|---|---|
| Budget | Built-up area (sq ft) × base cost per sq ft × location-tier cost factor |
| CapEx incurred | Estimated budget × completion percentage |
| Value on completion | Built-up area × base market rate × location-tier market factor |
| Current asset valuation | Value on completion × completion percentage, with a 10% risk discount until handover |
| Steel / cement | Per-square-foot benchmark by structure type, scaled by completion percentage |

Rates are indicative benchmarks defined in `STRUCTURE_TYPES` and `TIER_FACTORS` in `app.py`. Update them using current local market data before relying on the estimates.

## 🧰 Tech Stack

- **UI:** Streamlit with custom CSS
- **AI:** Google Gemini via the `google-genai` SDK (vision, JSON output, and chat)
- **Imaging:** Pillow
- **Concept renders:** Pollinations AI (URL-based; no API key required by this project)
- **Referenced standards:** OSHA 29 CFR 1926, IS 456:2000, NBC 2016

## 🔒 Privacy & Security

- The API key is held in session memory and is not intentionally stored or logged by the app.
- Uploaded images are processed in memory and sent to the Gemini API only when you run an analysis.
- The application has no database or app-managed persistent storage.
- Keep `.streamlit/secrets.toml` out of version control.

## ⚠️ Known Limitations

- Photo-based crack-width estimates are approximate. Including a coin or ruler for scale may help, but does not replace professional measurement.
- Model output may be wrong or incomplete. Verify references, findings, and recommendations before relying on them.
- Pollinations is a free third-party service and may be slow or unavailable.
- Gemini model names in the sidebar may need updating as Google releases new versions.
- This project is a demonstration aid, not a substitute for professional engineering inspection, certified valuation, or site-safety procedures.

## 🗺️ Roadmap

- [ ] Video and multi-image site walkthrough analysis
- [ ] PDF report export
- [ ] Bill of quantities (BOQ) estimator
- [ ] Multilingual (Hindi) assistant and alerts
- [ ] Live weather API integration

## 👤 Author

**Mohammad Anas Chhipa**  
*Skill Wallet Capstone Project 1*

## 📄 License

This project is intended to be released under the MIT License. Add a `LICENSE` file containing the MIT License text before presenting the repository as formally licensed.

Live weather API integration
👤 Author
Mayank Suryavanshi: Skill Wallet Capstone Project 1

📄 License
Released under the MIT License. Add a LICENSE file to your repository if you choose to publish under it.
