<h1>ML-based AI Governance Vision Predictor</h1>

<p class="subtitle">
  A machine learning decision-support tool for assessing AI governance vision
  and institutional readiness in public organisations
</p>

<p>
  <span class="badge">Python</span>
  <span class="badge">scikit-learn</span>
  <span class="badge">joblib</span>
  <span class="badge">Pandas</span>
</p>

<p>
  This project was developed as part of an academic study on artificial intelligence
  integration and governance readiness in public institutions.
</p>

<p>
  This repository provides a small, reproducible pipeline to:
</p>
<ul>
  <li>Load survey data (Excel / CSV)</li>
  <li>Compute <strong>AI Governance Vision</strong> (raw score and percentage)</li>
  <li>Load pre-trained machine learning models and predict vision indicators
      (<code>VUTAI1</code>, <code>VUTAI2</code>, <code>VUTAI3</code>)</li>
  <li>Aggregate predictions into an overall vision score and an interpretable level
      (Low / Moderate / High)</li>
</ul>

<div class="note">
  <strong>What this tool predicts</strong><br/>
  The machine learning models output predicted values for
  <code>VUTAI1</code>, <code>VUTAI2</code>, and <code>VUTAI3</code>.
  These three predicted items are then used to compute:
  <ul>
    <li><code>AI_Governance_Vision</code> (mean on the 1–4 Likert scale)</li>
    <li><code>AI_Governance_Vision_Pct</code> (normalised to 0–100%)</li>
    <li><code>Vision_Level</code> (Low / Moderate / High)</li>
  </ul>
</div>

<h2>Project structure</h2>
<pre><code>integrationAIPLS/
├─ ML-Predict.ipynb          # Main prediction workflow
├─ ML-Train.ipynb            # (Optional) model training workflow
├─ Models/                   # Saved .joblib models (one per target)
│  ├─ ML_BestModel_VUTAI_VUTAI1_*.joblib
│  ├─ ML_BestModel_VUTAI_VUTAI2_*.joblib
│  └─ ML_BestModel_VUTAI_VUTAI3_*.joblib
├─ Results/                  # Exported figures and tables (SVG / PDF)
         
</code></pre>

<h2>Requirements</h2>
<p>Create a clean environment (recommended) and install dependencies.</p>

<h3>Option A: pip</h3>
<pre><code>pip install pandas numpy scikit-learn joblib matplotlib openpyxl</code></pre>

<h3>Option B: conda</h3>
<pre><code>conda create -n ai-vision python=3.11 -y
conda activate ai-vision
conda install -c conda-forge pandas numpy scikit-learn joblib matplotlib openpyxl -y</code></pre>

<div class="warn">
  <strong>scikit-learn version warning</strong><br/>
  Models trained with a different scikit-learn version may trigger a warning during
  <code>joblib.load()</code>. This does not affect predictions but version pinning
  is recommended for strict reproducibility.
</div>

<h2>How to use (prediction)</h2>

<p>
  The main entry point of the project is <strong>ML-Predict.ipynb</strong>,
  which contains the complete prediction and scoring pipeline.
</p>

<h3>1) Place trained models in <code>Models/</code></h3>
<pre><code>ML_BestModel_VUTAI_{target}_*.joblib</code></pre>

<h3>2) Prepare input data</h3>
<p>The input must contain the same features used during training:</p>
<pre><code>FEATURE_ORDER = [
  "EST1", "EST3", "EST4",
  "OUAI2", "OUAI3", "OUAI4",
  "PBUG1", "PBUG2", "PBUG3", "PBUG4"
]</code></pre>

<h3>3) Run the notebook</h3>
<ul>
  <li>Open <code>ML-Predict.ipynb</code></li>
  <li>Run cells sequentially (data → models → prediction → output)</li>
</ul>

<h2>Outputs</h2>
<ul>
  <li>Predicted vision indicators: <code>VUTAI1</code>, <code>VUTAI2</code>, <code>VUTAI3</code></li>
  <li>Overall vision score: <code>AI_Governance_Vision</code> (1–4)</li>
  <li>Percentage score: <code>AI_Governance_Vision_Pct</code></li>
  <li>Interpretation: <code>Vision_Level</code> (Low / Moderate / High)</li>
</ul>

<h2>Reproducibility notes</h2>
<ul>
  <li>Keep feature names and order consistent with training.</li>
  <li>Pin package versions for long-term reproducibility.</li>
</ul>

<h2>Data privacy</h2>
<p>
  Data is provided upon request.
</p>
