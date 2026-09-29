# MLOps with Marimo and MLflow 🚀

A lightweight, reproducible MLOps environment that combines the reactive, pure-Python execution of [Marimo notebooks](https://marimo.io/) with the robust experiment tracking and model management of [MLflow](https://mlflow.org/).

## 🌟 Overview

This repository provides a foundational template for developing machine learning models interactively while maintaining strict tracking of experiments, parameters, and artifacts. 

- **Marimo** ensures your notebooks are reproducible, version-controllable (saved as pure Python scripts), and free from hidden state issues.
- **MLflow** handles the backend logging of metrics, hyperparameters, and model artifacts, making it easy to compare runs and transition models to production.

## 📁 Project Structure

```text
.
├── notebooks/          # Marimo notebooks (.py files)
├── src/                # Reusable Python modules (data prep, model definitions)
├── data/               # Raw and processed datasets
├── mlruns/             # Local MLflow tracking directory (auto-generated)
├── requirements.txt    # Project dependencies
└── README.md
```

## 🛠️ Prerequisites & Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/samueladole/mlops.git
   cd mlops
   ```

2. **Set up a virtual environment (recommended):**
   ```bash
   # Install uv if you haven't already (or use pip install uv)
   curl -LsSf https://astral.sh/uv/install.sh | sh

   # Create and configure the environment
   uv venv
   source .venv/bin/activate  # On Windows use `.venv\Scripts\activate`
   ```

## 🚀 Quick Start

### 1. Start the MLflow Tracking Server
Open a terminal and start the MLflow UI to track your experiments locally:
```bash
mlflow ui --port 5000
```
*The MLflow dashboard will be available at `http://localhost:5000`.*

### 2. Launch Marimo
In a new terminal window, start the Marimo editor:
```bash
marimo edit notebooks/train_model.py
```

### 3. Example Workflow
Inside your Marimo notebook, you can seamlessly integrate MLflow tracking:

```python
import marimo
import mlflow
import sklearn

app = marimo.App()

@app.cell
def train_model():
    mlflow.set_tracking_uri("http://localhost:5000")
    mlflow.set_experiment("Marimo_Experiment")
    
    with mlflow.start_run():
        # Your training code here
        params = {"n_estimators": 100, "max_depth": 5}
        mlflow.log_params(params)
        
        # Train model...
        accuracy = 0.95 
        mlflow.log_metric("accuracy", accuracy)
        
        # Log model...
        # mlflow.sklearn.log_model(model, "model")
        
    return params, accuracy
```

## 🤝 Contributing
Contributions, issues, and feature requests are welcome! Feel free to check the issues page.