---
title: Machine Learning and Data in Operation
authors:
  - name: Dr. Frank-Peter Schilling
    affiliation: ZHAW School of Engineering
  - name: Vanni Galli
    affiliation: SUPSI
exports:
- format: pdf
  template: https://github.com/marbetschar/plain_latex_article/archive/refs/heads/main.zip
  output: Machine-Learning-and-Data-in-Operation.pdf
  id: mlops-pdf
downloads:
  - id: mlops-pdf
    title: Download as PDF
---

## Introduction to MLOps

### Learning Objectives
- Recognize the **complete lifecycle** of machine learning projects
- Understand **MLOps as an extension of DevOps** tailored for ML
- Identify **ML product archetypes** (Software 2.0, Human in the Loop, Autonomous Systems)
- Distinguish between **ML in Research vs ML in Production**
- Understand the **iterative ML project lifecycle** and the "Data FlyWheel"

### Key Concepts
```{admonition} MLOps Definition
:class: note
**MLOps** (Machine Learning Operations) is:
1. The extension of DevOps to ML projects
2. A set of tools and best practices for bringing ML into production
3. A systems approach considering ML holistically
```
#### ML Project Lifecycle
```{mermaid}
:align: center
flowchart LR
    A[Data Collection] --> B[Data Preparation]
    B --> C[Model Development]
    C --> D[Model Training]
    D --> E[Model Evaluation]
    E --> F[Model Deployment]
    F --> G[Monitoring]
    G -->|Feedback| A
    G -->|Retraining| D
```
#### ML Product Archetypes
1. **Software 2.0**: Humans specify goals; algorithm searches for program that works
2. **Human in the Loop**: ML assists human decision-making
3. **Autonomous Systems**: ML makes decisions independently
#### ML Research vs Production
```{list-table}
:header: Aspect, Research, Production
:widths: 20 40 40
* - Goal
  - Publish novel results
  - Build reliable, scalable systems
* - Data
  - Clean, curated datasets
  - Messy, real-world data
* - Evaluation
  - Accuracy on test set
  - Performance, latency, robustness
* - Iteration
  - Experimental
  - Incremental, controlled
* - Focus
  - Model innovation
  - System reliability
```

## Deep Learning Recap
### Learning Objectives
- **Know**: Distinctions between AI, ML, and DL; supervised vs unsupervised learning
- **Know**: Building blocks of neural networks and training via backpropagation
- **Know**: CNN architectures (ResNet, VGG) and transformer networks
- **Know**: How deep learning-based image classification works
- **Know**: Self-attention mechanism and transformer layout
- **Apply**: Deep Learning with PyTorch (train and optimize neural networks)
### Key Concepts
#### Neural Network Fundamentals
- **Forward Pass**: Input → Hidden Layers → Output
- **Backpropagation**: Compute gradients using chain rule
- **Gradient Descent**: Update weights to minimize loss
- **Loss Functions**: MSE, Cross-Entropy, etc.
- **Optimizers**: SGD, Adam, RMSprop
- **Regularization**: Dropout, Weight Decay, BatchNorm
#### CNN Architectures
- **AlexNet**: Pioneered deep CNNs (2012)
- **VGG**: Uniform architecture with small 3x3 filters
- **ResNet**: Residual connections for deep networks
- **Transformer**: Self-attention mechanism for sequential data

### Code Examples

::::{dropdown} PyTorch Neural Network (FashionMNIST)
```python
import torch
import torch.nn as nn
import torch.optim as optim
from torch.utils.data import DataLoader
from torchvision import datasets, transforms
# Define a simple neural network
class NeuralNetwork(nn.Module):
    def __init__(self):
        super(NeuralNetwork, self).__init__()
        self.flatten = nn.Flatten()
        self.linear_relu_stack = nn.Sequential(
            nn.Linear(28*28, 512),  # Input layer (28x28 images)
            nn.ReLU(),
            nn.Linear(512, 512),     # Hidden layer
            nn.ReLU(),
            nn.Linear(512, 10),     # Output layer (10 classes)
        )
    def forward(self, x):
        x = self.flatten(x)  # Flatten 28x28 image to 784 features
        logits = self.linear_relu_stack(x)
        return logits
# Initialize model, loss function, and optimizer
model = NeuralNetwork()
loss_fn = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)
# Load data
transform = transforms.ToTensor()
training_data = datasets.FashionMNIST(
    root="data",
    train=True,
    download=True,
    transform=transform
)
train_dataloader = DataLoader(training_data, batch_size=64, shuffle=True)
# Training loop
for epoch in range(5):
    for batch_idx, (data, target) in enumerate(train_dataloader):
        # Forward pass
        pred = model(data)
        loss = loss_fn(pred, target)
        
        # Backward pass
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
        
        if batch_idx % 100 == 0:
            print(f"Epoch {epoch}, Batch {batch_idx}, Loss: {loss.item():.4f}")
```
::::

::::{dropdown} PyTorch Lightning Autoencoder
```python
import pytorch_lightning as pl
import torch
import torch.nn as nn
import torch.nn.functional as F
from torch.utils.data import DataLoader, random_split
from torchvision import datasets, transforms
# Define Lightning Module
class LitAutoEncoder(pl.LightningModule):
    def __init__(self):
        super().__init__()
        # Encoder: Input (784) -> Hidden (64) -> Latent (3)
        self.encoder = nn.Sequential(
            nn.Linear(28 * 28, 64),
            nn.ReLU(),
            nn.Linear(64, 3)  # 3-dimensional latent space
        )
        # Decoder: Latent (3) -> Hidden (64) -> Output (784)
        self.decoder = nn.Sequential(
            nn.Linear(3, 64),
            nn.ReLU(),
            nn.Linear(64, 28 * 28)
        )
    def forward(self, x):
        # Flatten input
        x = x.view(x.size(0), -1)
        embedding = self.encoder(x)
        return embedding
    def configure_optimizers(self):
        # Automatic optimization
        return optim.Adam(self.parameters(), lr=1e-3)
    def training_step(self, train_batch, batch_idx):
        x, _ = train_batch
        x = x.view(x.size(0), -1)  # Flatten
        z = self.encoder(x)     # Encode
        x_hat = self.decoder(z)  # Decode
        loss = F.mse_loss(x_hat, x)  # Reconstruction loss
        self.log('train_loss', loss)  # Log for TensorBoard
        return loss
# Setup data
dataset = datasets.MNIST('', train=True, download=True, transform=transforms.ToTensor())
mnist_train, mnist_val = random_split(dataset, [55000, 5000])
train_loader = DataLoader(mnist_train, batch_size=32)
val_loader = DataLoader(mnist_val, batch_size=32)
# Train
model = LitAutoEncoder()
trainer = pl.Trainer(gpus=4, precision=16, limit_train_batches=0.5)
trainer.fit(model, train_loader, val_loader)
```
::::

## Infrastructure & Tooling
### Learning Objectives
- **Know**: Software development environment for ML
- **Know**: Main ML and DL frameworks (PyTorch, TensorFlow, JAX) and their benefits
- **Know**: Model Zoos and pre-trained models
- **Know**: Distributed training paradigms (data & model parallelism)
- **Know**: Resource and workload management (containers vs VMs)
- **Know**: Experiment and model tracking tools
- **Know**: All-in-one ML solutions (Hugging Face, Streamlit, MLflow)
- **Apply**: Build web apps and chatbots using Streamlit
### Key Concepts
#### ML Frameworks Comparison
```{list-table}
:header: Framework, Strengths, Use Cases
:widths: 20 40 40
* - **PyTorch**
  - Excellent dev experience, production-ready, great ecosystem
  - Research, production, mobile deployment
* - **TensorFlow**
  - Strong distributed training, TensorBoard integration
  - Large-scale production, enterprise
* - **JAX**
  - Functional programming, automatic differentiation
  - Research, numerical computing
* - **Hugging Face**
  - Pre-trained models, easy fine-tuning
  - NLP, transformers, quick prototyping
```
#### Containers vs Virtual Machines
```{list-table}
:header: Aspect, Containers, Virtual Machines
:widths: 20 40 40
* - **Isolation**
  - Process-level
  - OS-level
* - **Overhead**
  - Low (shares host OS)
  - High (full OS)
* - **Boot Time**
  - Seconds
  - Minutes
* - **Portability**
  - High
  - Medium (OS-specific)
* - **Use Case**
  - Microservices, ML serving
  - Full environments, legacy apps
```
#### All-in-One ML Solutions
- **Hugging Face**: Transformers, datasets, inference API
- **Streamlit**: Web apps for ML/Data Science
- **MLflow**: Experiment tracking, model registry
- **Lightning.ai**: PyTorch Lightning ecosystem
### Code Examples

::::{dropdown} Streamlit Web App
```python
import streamlit as st
import torch
from transformers import pipeline
# Set page title and layout
st.set_page_config(page_title="ML Chatbot", layout="wide")
# Title
st.title("🤖 ML Chatbot Demo")
# Sidebar for model selection
with st.sidebar:
    st.header("Settings")
    model_name = st.selectbox(
        "Choose a model",
        ["distilbert-base-uncased", "bert-base-uncased"]
    )
# Load model (cached for performance)
@st.cache_resource
def load_model(model_name):
    # Load text generation pipeline
    generator = pipeline(
        "text-generation",
        model=model_name,
        device=0 if torch.cuda.is_available() else -1
    )
    return generator
model = load_model(model_name)
# User input
user_input = st.text_input("Enter your prompt:", "Once upon a time,")
if user_input:
    # Generate response
    with st.spinner("Generating response..."):
        result = model(
            user_input,
            max_length=100,
            num_return_sequences=1
        )
    
    # Display result
    st.subheader("Generated Text:")
    st.write(result[0]['generated_text'])
# Add expandable info
with st.expander("ℹ️ About"):
    st.write("This is a simple Streamlit chatbot using Hugging Face Transformers.")
    st.write(f"Current model: {model_name}")
```
::::

::::{dropdown} Dockerfile for ML Application
```dockerfile
# Start from official PyTorch base image with CUDA support
FROM pytorch/pytorch:2.0.1-cuda11.7-cudnn8-runtime
# Set maintainer label
LABEL maintainer="your.name@zhaw.ch"
# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*
# Install Python packages
RUN pip install --no-cache-dir \
    torch \
    transformers \
    streamlit \
    pandas \
    numpy
# Copy application code
WORKDIR /app
COPY . .
# Expose port for Streamlit
EXPOSE 8501
# Set default command
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```
::::

## Development & Troubleshooting
### Learning Objectives
- **Know**: Decision tree for debugging ML/DL models
- **Know**: Essential components: Start simple, implement & debug, improve turnaround, evaluate
- **Know**: Important concepts: bias-variance decomposition, data distribution shift
- **Know**: Hyperparameter optimization techniques (grid search, random search)
- **Apply**: Debugging strategies to own ML projects
- **Apply**: Run hyperparameter sweeps with Weights & Biases or Ray Tune
### Key Concepts
#### Debugging Decision Tree
```{mermaid}
:align: center
flowchart LR
    A[Model Performance Poor?] --> B{Is it a bug?}
    B -->|Yes| C[Fix implementation bug]
    B -->|No| D[Evaluate on dev set]
    D --> E{Bias High?}
    E -->|Yes| F[Improve model/data]
    E -->|No| G{Variance High?}
    G -->|Yes| H[Get more data/regularize]
    G -->|No| I[Good performance!]
```
#### Bias-Variance Tradeoff
- **High Bias (Underfitting)**: Model is too simple, misses patterns
  - *Solution*: Increase model complexity, add features
- **High Variance (Overfitting)**: Model memorizes training data
  - *Solution*: Get more data, regularize, simplify model
- **Good Fit**: Low bias and low variance
#### Hyperparameter Optimization
- **Grid Search**: Exhaustive search over specified values
- **Random Search**: Random sampling from distributions
- **Bayesian Optimization**: Model-based optimization
- **Evolutionary Methods**: Genetic algorithms
### Code Examples

::::{dropdown} MLflow Experiment Tracking
```python
import mlflow
import mlflow.pytorch
from mlflow.models import infer_signature
import torch
import torch.nn as nn
from torch.utils.data import DataLoader
from torchvision import datasets, transforms
# Start MLflow run
mlflow.set_experiment("FashionMNIST_Training")
with mlflow.start_run():
    # Log parameters
    mlflow.log_param("learning_rate", 0.001)
    mlflow.log_param("batch_size", 64)
    mlflow.log_param("epochs", 5)
    mlflow.log_param("model", "SimpleNN")
    
    # Define model (same as Lecture 02)
    class NeuralNetwork(nn.Module):
        def __init__(self):
            super().__init__()
            self.flatten = nn.Flatten()
            self.linear_relu_stack = nn.Sequential(
                nn.Linear(28*28, 512),
                nn.ReLU(),
                nn.Linear(512, 512),
                nn.ReLU(),
                nn.Linear(512, 10)
            )
        
        def forward(self, x):
            return self.linear_relu_stack(self.flatten(x))
    
    # Initialize
    model = NeuralNetwork()
    loss_fn = nn.CrossEntropyLoss()
    optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
    
    # Load data
    transform = transforms.ToTensor()
    train_data = datasets.FashionMNIST(root="data", train=True, download=True, transform=transform)
    train_loader = DataLoader(train_data, batch_size=64, shuffle=True)
    
    # Training loop
    for epoch in range(5):
        for batch_idx, (data, target) in enumerate(train_loader):
            pred = model(data)
            loss = loss_fn(pred, target)
            
            optimizer.zero_grad()
            loss.backward()
            optimizer.step()
            
            # Log loss every 100 batches
            if batch_idx % 100 == 0:
                mlflow.log_metric("loss", loss.item(), step=epoch * len(train_loader) + batch_idx)
    
    # Log model
    example_input = torch.randn(1, 1, 28, 28)
    signature = infer_signature(model, example_input)
    mlflow.pytorch.log_model(model, "model", signature=signature)
    
    # Log artifacts (e.g., plots)
    mlflow.log_artifact("plots/training_curve.png")
print(f"Run ID: {mlflow.active_run().info.run_id}")
```
::::

::::{dropdown} Ray Tune Hyperparameter Optimization
```python
from ray import tune
from ray.tune import CLIReporter
from ray.tune.schedulers import ASHAScheduler
import torch
import torch.nn as nn
from torch.utils.data import DataLoader
from torchvision import datasets, transforms
# Define model with configurable hyperparameters
class NeuralNetwork(nn.Module):
    def __init__(self, l1_size, l2_size):
        super().__init__()
        self.flatten = nn.Flatten()
        self.linear_relu_stack = nn.Sequential(
            nn.Linear(28*28, l1_size),
            nn.ReLU(),
            nn.Linear(l1_size, l2_size),
            nn.ReLU(),
            nn.Linear(l2_size, 10)
        )
    
    def forward(self, x):
        return self.linear_relu_stack(self.flatten(x))
# Training function for Ray Tune
def train_model(config):
    # Load data
    transform = transforms.ToTensor()
    train_data = datasets.FashionMNIST(root="data", train=True, download=True, transform=transform)
    train_loader = DataLoader(train_data, batch_size=config["batch_size"], shuffle=True)
    
    # Initialize model
    model = NeuralNetwork(
        l1_size=config["l1_size"],
        l2_size=config["l2_size"]
    )
    loss_fn = nn.CrossEntropyLoss()
    optimizer = torch.optim.Adam(model.parameters(), lr=config["lr"])
    
    # Training loop
    for epoch in range(config["epochs"]):
        for batch_idx, (data, target) in enumerate(train_loader):
            pred = model(data)
            loss = loss_fn(pred, target)
            
            optimizer.zero_grad()
            loss.backward()
            optimizer.step()
            
            # Report intermediate results
            if batch_idx % 100 == 0:
                tune.report(loss=loss.item())
# Define search space
config = {
    "l1_size": tune.choice([128, 256, 512]),
    "l2_size": tune.choice([64, 128, 256]),
    "lr": tune.loguniform(1e-4, 1e-2),
    "batch_size": tune.choice([32, 64, 128]),
    "epochs": 3
}
# Configure and run
scheduler = ASHAScheduler(
    max_t=10,  # Max epochs
    grace_period=1,  # Min epochs before early stopping
    reduction_factor=2  # Reduce resources by factor of 2
)
reporter = CLIReporter(
    metric_columns=["loss", "training_iteration"]
)
analysis = tune.run(
    train_model,
    search_alg=tune.BasicVariantGenerator(),
    scheduler=scheduler,
    config=config,
    num_samples=10,  # Number of trials
    resources_per_trial={"cpu": 2, "gpu": 1},
    progress_reporter=reporter
)
# Get best trial
best_trial = analysis.get_best_trial(metric="loss", mode="min")
print(f"Best trial config: {best_trial.config}")
print(f"Best trial loss: {best_trial.last_result['loss']}")
```
::::

## Testing
### Learning Objectives
- **Know**: Concepts and tools for software testing
- **Know**: CI/CD paradigm and task automation
- **Familiar**: Methods to test ML systems holistically
- **Familiar**: Performance envelope understanding
- **Apply**: Implement testing and automation in practice
### Key Concepts
#### Testing Pyramid
```{mermaid}
:align: center
graph TD
    A[Unit Tests] --> B[Integration Tests]
    B --> C[End-to-End Tests]
    D[ML-Specific Tests] --> B
    
    style A fill:#4CAF50,stroke:#388E3C
    style B fill:#2196F3,stroke:#1976D2
    style C fill:#9C27B0,stroke:#7B1FA2
    style D fill:#FF9800,stroke:#F57C00
```
#### Testing Levels
1. **Unit Testing**: Test individual functions/classes
2. **Integration Testing**: Test component interactions
3. **End-to-End Testing**: Test complete workflows
4. **ML-Specific Testing**:
   - Data validation tests
   - Model performance tests
   - Fairness tests
   - Robustness tests
#### CI/CD Pipeline
- **Continuous Integration**: Automatically build and test on code changes
- **Continuous Delivery**: Automatically deploy to staging
- **Continuous Deployment**: Automatically deploy to production
### Code Examples

::::{dropdown} Unit Testing with pytest
```python
# test_model.py
import pytest
import torch
from model import NeuralNetwork  # Assuming model is defined in model.py
@pytest.fixture
def sample_model():
    """Fixture providing a fresh model instance for each test."""
    return NeuralNetwork()
def test_model_forward(sample_model):
    """Test that model forward pass works with correct input shape."""
    # Create dummy input (batch_size=1, channels=1, height=28, width=28)
    x = torch.randn(1, 1, 28, 28)
    
    # Forward pass should not raise exception
    output = sample_model(x)
    
    # Check output shape (batch_size=1, num_classes=10)
    assert output.shape == (1, 10), f"Expected shape (1, 10), got {output.shape}"
def test_model_parameters(sample_model):
    """Test that model has expected number of parameters."""
    param_count = sum(p.numel() for p in sample_model.parameters())
    # SimpleNN: (28*28 * 512) + 512 + (512 * 512) + 512 + (512 * 10) + 10
    # = 393,216 + 512 + 262,144 + 512 + 5,120 + 10 = 661,414
    assert param_count == 661414, f"Expected 661,414 parameters, got {param_count}"
class TestTraining:
    """Test training-related functionality."""
    
    def test_loss_decreases(self):
        """Test that loss decreases during training."""
        # Setup
        model = NeuralNetwork()
        optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
        loss_fn = torch.nn.CrossEntropyLoss()
        
        # Create dummy data
        x = torch.randn(32, 1, 28, 28)
        y = torch.randint(0, 10, (32,))
        
        # Get initial loss
        pred = model(x)
        initial_loss = loss_fn(pred, y).item()
        
        # Training step
        optimizer.zero_grad()
        loss = loss_fn(pred, y)
        loss.backward()
        optimizer.step()
        
        # Get new loss
        pred = model(x)
        new_loss = loss_fn(pred, y).item()
        
        # Loss should decrease (or stay same, but not increase significantly)
        assert new_loss <= initial_loss * 1.1, \
            f"Loss increased from {initial_loss} to {new_loss}"
```
::::

::::{dropdown} GitHub Actions CI/CD Pipeline
```yaml
name: ML Pipeline CI/CD
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout repository
      uses: actions/checkout@v4
    
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install pytest torch torchvision
    
    - name: Run unit tests
      run: |
        python -m pytest tests/ -v --tb=short
    
    - name: Run linting
      run: |
        pip install flake8 black
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
        black --check .
  train:
    needs: test
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout repository
      uses: actions/checkout@v4
    
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install torch torchvision mlflow
    
    - name: Train model
      run: |
        python train.py
    
    - name: Upload artifacts
      uses: actions/upload-artifact@v3
      with:
        name: model-artifacts
        path: |
          models/
          mlruns/
```
::::

## Data Engineering
### Learning Objectives
- **Know**: Real-world challenges of obtaining high-quality training data
- **Know**: Main concepts, methods & tools for data sources and storage
- **Know**: Main types of data formats and databases
- **Know**: Feature stores and data exploration
- **Familiar**: Workflow processing as DAGs
- **Familiar**: Common workflow management tools
- **Familiar**: Different ways to implement data versioning
- **Apply**: Perform exploratory data analysis
- **Apply**: Apply data versioning and data augmentation in practice
### Key Concepts
#### Data Storage Options
```{list-table}
:header: Type, Description, Use Cases, Examples
:widths: 15 30 25 25
* - **Filesystem**
  - Simple file storage on disk
  - Local development, small datasets
  - CSV, JSON, Parquet
* - **Object Storage**
  - Scalable, distributed file storage
  - Large datasets, cloud storage
  - S3, GCS, Azure Blob
* - **Databases**
  - Structured data with query capabilities
  - Transactional data, metadata
  - PostgreSQL, MySQL
* - **Data Lakes**
  - Centralized repositories for raw data
  - Big data, analytics
  - Delta Lake, Iceberg
* - **Data Warehouses**
  - Optimized for analytics
  - Business intelligence
  - BigQuery, Snowflake
```
#### Data Processing Workflows
- **DAG (Directed Acyclic Graph)**: Workflow representation where nodes are tasks and edges are dependencies
- **Workflow Managers**: Tools to orchestrate data pipelines
  - **Airflow**: Most popular, configuration-as-code (Python)
  - **Spark**: Distributed processing, in-memory computation
  - **Metaflow**: Python/R workflows, AWS Batch integration
  - **Ploomber**: Lightweight, Jupyter-native
#### Feature Stores
- **Purpose**: Centralized repository for ML features
- **Benefits**:
  - Avoid feature recomputation
  - Ensure consistency between training and inference
  - Share features across teams
- **Examples**: Feast, Tecton, Hopsworks
#### Data Versioning
- **Git LFS**: Large File Storage for Git
- **DVC**: Data Version Control (like Git for data)
- **Specialized Tools**: Oxen, LakeFS
### Code Examples

::::{dropdown} Apache Airflow DAG
```python
from datetime import datetime, timedelta
from airflow import DAG
from airflow.operators.bash import BashOperator
from airflow.operators.python import PythonOperator
from airflow.operators.docker import DockerOperator
import time
# Default arguments for the DAG
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'email': ['your.email@zhaw.ch'],
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}
# Define the DAG
dag = DAG(
    'ml_data_pipeline',
    default_args=default_args,
    description='ML Data Processing Pipeline',
    schedule_interval=timedelta(days=1),  # Run daily
    start_date=datetime(2026, 1, 1),
    catchup=False,
    tags=['mlops', 'data'],
)
# Task 1: Print current date
t1 = BashOperator(
    task_id='print_date',
    bash_command='date',
    dag=dag,
)
# Task 2: Data validation
def validate_data():
    import pandas as pd
    from pathlib import Path
    
    # Check if data file exists
    data_path = Path("/data/raw/dataset.csv")
    if not data_path.exists():
        raise FileNotFoundError(f"Data file not found: {data_path}")
    
    # Load and validate
    df = pd.read_csv(data_path)
    assert len(df) > 0, "Dataset is empty"
    assert 'target' in df.columns, "Target column missing"
    
    print(f"Data validation passed. Shape: {df.shape}")
t2 = PythonOperator(
    task_id='validate_data',
    python_callable=validate_data,
    dag=dag,
)
# Task 3: Preprocessing in Docker
t3 = DockerOperator(
    task_id='preprocess_data',
    image='mlops/preprocessor:latest',
    command='python /app/preprocess.py /data/raw/dataset.csv /data/processed/',
    docker_url='unix://var/run/docker.sock',  # Use local Docker
    network_mode='bridge',
    dag=dag,
)
# Task 4: Split data
def split_data():
    import pandas as pd
    from sklearn.model_selection import train_test_split
    
    df = pd.read_csv("/data/processed/clean_data.csv")
    train, test = train_test_split(df, test_size=0.2, random_state=42)
    
    train.to_csv("/data/processed/train.csv", index=False)
    test.to_csv("/data/processed/test.csv", index=False)
    
    print(f"Train size: {len(train)}, Test size: {len(test)}")
t4 = PythonOperator(
    task_id='split_data',
    python_callable=split_data,
    dag=dag,
)
# Define task dependencies
t1 >> t2 >> t3 >> t4
```
::::

::::{dropdown} Data Versioning with DVC
```python
# dvc.yaml - DVC pipeline definition
stages:
  prepare:
    cmd: python src/data/prepare.py
    deps:
    - src/data/prepare.py
    - data/raw
    outs:
    - data/processed
  train:
    cmd: python src/models/train.py
    deps:
    - src/models/train.py
    - data/processed
    params:
    - learning_rate
    - batch_size
    - epochs
    metrics:
    - metrics.json:
        cache: false
    outs:
    - models/model.pkl
  evaluate:
    cmd: python src/models/evaluate.py
    deps:
    - src/models/evaluate.py
    - models/model.pkl
    - data/processed
    metrics:
    - metrics.json:
        cache: false
```
```bash
# DVC commands
# Initialize DVC in your repository
dvc init
# Add data to DVC tracking
dvc add data/raw/dataset.csv
# Create and run pipeline
dvc repro
# Track metrics and parameters
dvc metrics show
dvc params show
# Push data to remote storage
dvc push
# Pull data from remote storage
dvc pull
```
::::

## Training Data & Feature Engineering
### Learning Objectives
- **Know**: Real-world challenges of obtaining sufficient high-quality training data
- **Know**: Important paradigms (self-supervised, semi-supervised learning)
- **Know**: Methods to generate labels from heuristics or active learning
- **Familiar**: Sampling techniques and counteracting class imbalance
- **Familiar**: Data augmentation and synthetic data generation methods
- **Familiar**: Motivation and main methods for feature engineering
- **Apply**: Data versioning, augmentation, and synthetic data generation in practice
### Key Concepts
#### Data Labeling Approaches
1. **Manual Labeling**
   - Domain experts label data
   - High quality but expensive and slow
   - Use annotation guidelines and QA processes
2. **Labeling Services**
   - Crowdsourcing (Amazon Mechanical Turk)
   - Professional services (Scale AI, Labelbox)
   - Cost-effective for large datasets
3. **Programmatic Labeling**
   - Use heuristics or rules to generate labels
   - Tools: Snorkel, Prodigy
   - Fast but may have lower quality
4. **Weak Supervision**
   - Combine multiple weak signals
   - Label Model approaches
   - Noisy but scalable
5. **Self-Supervised Learning**
   - Learn from data structure without labels
   - Pretext tasks (masked language modeling, contrastive learning)
   - Then fine-tune on labeled data
6. **Active Learning**
   - Model identifies uncertain samples
   - Human labels only the most informative samples
   - Reduces labeling effort
#### Handling Class Imbalance
- **Resampling Techniques**:
  - Oversampling minority class
  - Undersampling majority class
  - SMOTE (Synthetic Minority Oversampling)
- **Loss Function Modifications**:
  - Class weighting in loss function
  - Focal loss for hard examples
- **Stratified Sampling**: Ensure class balance in splits
#### Data Augmentation
- **Images**: Rotation, flipping, cropping, color jitter, noise
- **Text**: Synonym replacement, back translation, paraphrasing
- **Speech**: Pitch shift, time stretch, noise addition
- **Libraries**: Albumentations (images), nlpaug (text), audiomentations (audio)
#### Feature Engineering
- **Handling Missing Values**: Imputation, flagging, removal
- **Scaling**: Standardization, Normalization, Min-Max
- **Discretization**: Binning continuous variables
- **Categorical Features**: One-hot encoding, embeddings
- **Positional Embeddings**: For sequential data
- **Avoiding Data Leakage**: Don't use future information
### Code Examples

::::{dropdown} Data Augmentation with Albumentations
```python
import albumentations as A
from albumentations.pytorch import ToTensorV2
import cv2
import numpy as np
# Define augmentation pipeline
train_transform = A.Compose([
    # Geometric transformations
    A.HorizontalFlip(p=0.5),           # Flip horizontally with 50% probability
    A.VerticalFlip(p=0.2),             # Flip vertically with 20% probability
    A.Rotate(limit=15, p=0.5),          # Rotate by ±15 degrees
    A.RandomResizedCrop(224, 224, scale=(0.8, 1.0)),  # Random crop and resize
    
    # Color transformations
    A.RandomBrightnessContrast(p=0.2),  # Adjust brightness and contrast
    A.RandomGamma(p=0.2),               # Apply gamma correction
    A.CLAHE(p=0.2),                     # Contrast Limited Adaptive Histogram Equalization
    
    # Noise
    A.GaussNoise(var_limit=(10.0, 50.0), p=0.1),  # Add Gaussian noise
    
    # Normalization
    A.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),
    
    # Convert to PyTorch tensor
    ToTensorV2(),
])
# Test transform (no augmentation, only normalization)
test_transform = A.Compose([
    A.Resize(224, 224),
    A.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),
    ToTensorV2(),
])
# Example usage
image = cv2.imread("image.jpg")
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)  # Convert to RGB
# Apply augmentation
augmented = train_transform(image=image)
augmented_image = augmented["image"]  # Get augmented image
print(f"Original shape: {image.shape}")
print(f"Augmented shape: {augmented_image.shape}")
```
::::

::::{dropdown} Handling Class Imbalance
```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.utils import resample
from imblearn.over_sampling import SMOTE
from imblearn.under_sampling import RandomUnderSampler
# Load dataset
df = pd.read_csv("data.csv")
X = df.drop("target", axis=1)
y = df["target"]
# Check class distribution
print("Original class distribution:")
print(y.value_counts())
# Method 1: Random Oversampling
# Separate majority and minority classes
majority_class = y.mode()[0]
minority_df = df[df["target"] != majority_class]
majority_df = df[df["target"] == majority_class]
# Upsample minority class
minority_upsampled = resample(
    minority_df,
    replace=True,             # Sample with replacement
    n_samples=len(majority_df),  # Match majority class size
    random_state=42
)
# Combine majority with upsampled minority
df_upsampled = pd.concat([majority_df, minority_upsampled])
# Method 2: SMOTE (Synthetic Minority Oversampling)
smote = SMOTE(random_state=42)
X_resampled, y_resampled = smote.fit_resample(X, y)
# Method 3: Random Undersampling
under_sampler = RandomUnderSampler(random_state=42)
X_under, y_under = under_sampler.fit_resample(X, y)
# Method 4: Class Weighting in Model
# In scikit-learn
from sklearn.ensemble import RandomForestClassifier
# Calculate class weights
class_counts = np.bincount(y)
class_weights = {i: 1.0 / count for i, count in enumerate(class_counts)}
# Train model with class weights
model = RandomForestClassifier(
    class_weight=class_weights,
    random_state=42
)
model.fit(X, y)
# In PyTorch
import torch
from torch.utils.data import WeightedRandomSampler
# Calculate sample weights
sample_weights = [class_weights[label] for label in y]
sampler = WeightedRandomSampler(
    weights=sample_weights,
    num_samples=len(sample_weights),
    replacement=True
)
# Use sampler in DataLoader
train_loader = DataLoader(
    dataset,
    batch_size=64,
    sampler=sampler
)
```
::::

::::{dropdown} Feature Engineering Pipeline
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import FunctionTransformer
# Load data
df = pd.read_csv("data.csv")
# Define feature engineering steps
numeric_features = ['age', 'income', 'score']
categorical_features = ['gender', 'city']
target = 'target'
# Create transformers
numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),  # Fill missing values
    ('scaler', StandardScaler()),  # Standardize features
])
categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='most_frequent')),  # Fill missing categories
    ('onehot', OneHotEncoder(handle_unknown='ignore')),  # One-hot encode
])
# Define custom feature engineering functions
def create_interaction_features(df):
    """Create interaction features."""
    df = df.copy()
    df['age_income_ratio'] = df['age'] / (df['income'] + 1)  # Avoid division by zero
    return df
def create_polynomial_features(df):
    """Create polynomial features."""
    df = df.copy()
    df['age_squared'] = df['age'] ** 2
    df['income_squared'] = df['income'] ** 2
    return df
# Combine all transformers
preprocessor = ColumnTransformer(
    transformers=[
        ('num', numeric_transformer, numeric_features),
        ('cat', categorical_transformer, categorical_features),
    ]
)
# Full pipeline
feature_engineering_pipeline = Pipeline(steps=[
    ('custom_features', FunctionTransformer(create_interaction_features)),
    ('preprocessor', preprocessor),
])
# Apply pipeline
X = df.drop(target, axis=1)
y = df[target]
X_transformed = feature_engineering_pipeline.fit_transform(X)
# Get feature names
feature_names = numeric_features + \
    list(feature_engineering_pipeline.named_steps['preprocessor']
         .named_transformers_['cat']
         .named_steps['onehot']
         .get_feature_names_out(categorical_features))
print(f"Transformed shape: {X_transformed.shape}")
print(f"Feature names: {feature_names}")
```
::::

## Deployment
### Learning Objectives
- **Know**: Fundamental concepts of deploying ML models
- **Know**: How model prediction services work
- **Know**: Differences between batch and online predictions
- **Familiar**: Optimization techniques and model compression methods
- **Familiar**: Challenges and benefits of cloud vs edge deployment
- **Apply**: Implement a model service using REST API or MLOps tools
### Key Concepts
#### Model Serving Patterns
```{list-table}
:header: Pattern, Description, Use Cases, Latency
:widths: 15 30 25 10
* - **Batch Prediction**
  - Process multiple inputs at once
  - Offline processing, large datasets
  - Hours to days
* - **Online Prediction**
  - Process one input at a time
  - Real-time applications
  - Milliseconds to seconds
* - **Streaming**
  - Process continuous data streams
  - Real-time analytics
  - Seconds
```
#### Model Serving Frameworks
```{list-table}
:header: Framework, Language, Key Features
:widths: 20 15 65
* - **TorchServe**
  - Python
  - PyTorch native, REST/gRPC APIs, model versioning
* - **TensorFlow Serving**
  - C++/Python
  - High performance, supports multiple models, batching
* - **Ray Serve**
  - Python
  - Scalable, supports multiple frameworks, traffic splitting
* - **vLLM**
  - Python
  - Optimized for LLM inference, PagedAttention
* - **MLServer**
  - Python
  - Framework-agnostic, REST API, model runtime
```
#### Deployment Options
```{list-table}
:header: Option, Pros, Cons
:widths: 15 40 40
* - **Cloud (Managed)**
  - Fully managed, scalable, high availability
  - Vendor lock-in, cost, cold start latency
* - **Cloud (Self-managed)**
  - Full control, portable
  - More work, need to manage infrastructure
* - **On-Premises**
  - Full control, data privacy
  - High upfront cost, maintenance
* - **Edge**
  - Low latency, offline capability
  - Limited resources, harder to update
* - **Serverless**
  - Auto-scaling, pay-per-use
  - Cold starts, limited execution time
```
#### Model Compression Techniques
1. **Quantization**: Reduce precision of weights (FP32 → INT8)
2. **Pruning**: Remove unimportant weights/neurons
3. **Knowledge Distillation**: Train smaller model to mimic larger one
4. **Low-Rank Optimization**: Factorize weight matrices
5. **Model Architecture**: Use more efficient architectures

### Code Examples

::::{dropdown} FastAPI Model Serving
```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
import torch
import torch.nn as nn
from typing import List
import logging
# Set up logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)
# Load model
class NeuralNetwork(nn.Module):
    def __init__(self):
        super().__init__()
        self.flatten = nn.Flatten()
        self.linear_relu_stack = nn.Sequential(
            nn.Linear(28*28, 512),
            nn.ReLU(),
            nn.Linear(512, 512),
            nn.ReLU(),
            nn.Linear(512, 10),
        )
    
    def forward(self, x):
        return self.linear_relu_stack(self.flatten(x))
# Load trained model
model = NeuralNetwork()
model.load_state_dict(torch.load("model.pth", map_location=torch.device('cpu')))
model.eval()  # Set to evaluation mode
# Define request/response models
class PredictionInput(BaseModel):
    """Input data for prediction."""
    X: List[List[float]]  # 28x28 flattened image
    
class PredictionOutput(BaseModel):
    """Output prediction."""
    y: List[int]  # Predicted class indices
    probabilities: List[List[float]]  # Class probabilities
# Create FastAPI app
app = FastAPI(
    title="FashionMNIST Classifier API",
    description="API for classifying FashionMNIST images",
    version="1.0.0"
)
@app.post("/predict", response_model=PredictionOutput)
async def predict(data: PredictionInput):
    """
    Make prediction on input data.
    
    Args:
        data: PredictionInput containing flattened 28x28 image
        
    Returns:
        PredictionOutput with predicted classes and probabilities
    """
    try:
        # Convert input to tensor
        x = torch.tensor(data.X, dtype=torch.float32)
        
        # Add batch dimension
        if len(x.shape) == 1:
            x = x.unsqueeze(0)
        
        # Make prediction
        with torch.no_grad():
            logits = model(x)
            probabilities = torch.softmax(logits, dim=1).tolist()
            predictions = torch.argmax(logits, dim=1).tolist()
        
        logger.info(f"Prediction completed for {len(predictions)} samples")
        
        return {
            "y": predictions,
            "probabilities": probabilities
        }
    
    except Exception as e:
        logger.error(f"Prediction failed: {str(e)}")
        raise HTTPException(status_code=400, detail=str(e))
@app.get("/health")
async def health_check():
    """Health check endpoint."""
    return {"status": "healthy"}
@app.get("/")
async def root():
    """Root endpoint with API info."""
    return {
        "message": "FashionMNIST Classifier API",
        "docs": "/docs",
        "health": "/health"
    }
if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
```
#### MLServer Model Serving
```python
# requirements.txt
mlserver
mlserver-mlflow
# model-settings.json
{
  "name": "fashion-mnist",
  "implementation": "mlserver_mlflow.MLflowRuntime",
  "parameters": {
    "uri": "models:/fashion-mnist/model",
    "version": "1"
  }
}
# settings.json
{
  "parallel_workers": 4,
  "batch_requests": true,
  "max_batch_size": 100,
  "max_batch_timeout": 10
}
# Dockerfile for MLServer
FROM python:3.10-slim
# Install MLServer and dependencies
RUN pip install mlserver mlserver-mlflow
# Copy model settings
COPY model-settings.json /models/fashion-mnist/
# Copy configuration
COPY settings.json /settings.json
# Set environment variables
ENV MLSERVER_MODEL_ROOT_PATH=/models
ENV MLSERVER_MODEL_CONFIG_ROOT_PATH=/models
# Expose port
EXPOSE 8080
# Start MLServer
CMD ["mlserver", "start", "--settings", "/settings.json"]
```
::::

::::{dropdown} Docker Deployment
```bash
# Dockerfile for FastAPI app
FROM python:3.10-slim
# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*
# Set working directory
WORKDIR /app
# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
# Copy application code
COPY . .
# Expose port
EXPOSE 8000
# Start FastAPI
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
# Build and run
# Build the Docker image
docker build -t fashion-mnist-api .
# Run the container
docker run -p 8000:8000 fashion-mnist-api
# Test the API
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{"X": [[0.1, 0.2, ...]]}'  # 784 values for 28x28 image
```
::::

## Monitoring & Continual Learning
### Learning Objectives
- **Familiar**: Concepts of data drift and model drift
- **Familiar**: Why monitoring is important in production
- **Familiar**: Main metrics to compare distributions
- **Familiar**: Main scenarios of retraining and continual learning
- **Familiar**: Approaches to continual learning
- **Apply**: Implement monitoring using simple metrics (data/model drift detection)
### Key Concepts
#### ML System Failures
1. **Data Drift**: Input data distribution changes
   - *Covariate Shift*: Features change, relationship stays same
   - *Label Shift*: Labels change, features stay same
   - *Concept Drift*: Relationship between features and labels changes
2. **Edge Cases**: Inputs outside training distribution
3. **Degenerate Feedback Loops**: Model decisions affect future data
4. **Cascading Errors**: Errors compound through pipeline
#### Monitoring Metrics
```{list-table}
:header: Category, Metrics, Tools
:widths: 20 50 30
* - **Operational**
  - Latency, throughput, availability, error rates
  - Prometheus, Grafana
* - **ML-Specific**
  - Prediction distribution, confidence scores, feature statistics
  - Evidently, Arize
* - **Data Quality**
  - Missing values, outliers, schema changes
  - Great Expectations, Deequ
* - **Model Performance**
  - Accuracy, precision, recall, F1, custom business metrics
  - MLflow, Weights & Biases
* - **Drift Detection**
  - KL divergence, JS divergence, Wasserstein distance, PSI
  - Alibi Detect, Evidently
```
#### Continual Learning Approaches
1. **Periodic Retraining**: Retrain model on schedule
2. **Trigger-Based Retraining**: Retrain when drift detected
3. **Online Learning**: Update model with each new sample
4. **Replay Methods**: Store old data and replay during training
5. **Regularization Methods**: Penalize changes to important weights
### Code Examples

::::{dropdown} Monitoring with Evidently
```python
import pandas as pd
from evidently.report import Report
from evidently.metric_preset import DataDriftPreset, ClassificationPreset
from evidently import ColumnMapping
# Load reference (training) and current (production) data
reference_data = pd.read_csv("data/train.csv")
current_data = pd.read_csv("data/production.csv")
# Define column mapping
column_mapping = ColumnMapping(
    target='target',
    prediction='prediction',
    numerical_features=['feature1', 'feature2', 'feature3'],
    categorical_features=['category1', 'category2']
)
# Create data drift report
report = Report(metrics=[
    DataDriftPreset(),
])
# Run calculation
report.run(
    reference_data=reference_data,
    current_data=current_data,
    column_mapping=column_mapping
)
# Save report
report.save_html("reports/data_drift.html")
# Create classification performance report
classification_report = Report(metrics=[
    ClassificationPreset(),
])
classification_report.run(
    reference_data=reference_data,
    current_data=current_data,
    column_mapping=column_mapping
)
classification_report.save_html("reports/classification.html")
# Check if drift detected
from evidently.calculations.data_drift import calculate_data_drift
result = calculate_data_drift(
    reference_data=reference_data,
    current_data=current_data,
    column_mapping=column_mapping
)
if result['dataset_drift']:
    print("⚠️  Data drift detected!")
else:
    print("✅ No data drift detected")
```
::::

::::{dropdown} Statistical Drift Detection
```python
import numpy as np
from scipy import stats
from scipy.stats import ks_2samp, wasserstein_distance, entropy
# Sample data: reference and current feature distributions
reference_feature = np.random.normal(0, 1, 1000)
current_feature = np.random.normal(0.5, 1, 1000)  # Shifted mean
def detect_drift(reference, current, threshold=0.05):
    """
    Detect drift using multiple statistical tests.
    
    Args:
        reference: Reference distribution (training data)
        current: Current distribution (production data)
        threshold: Significance level
        
    Returns:
        dict: Test results and drift detection
    """
    results = {}
    
    # Kolmogorov-Smirnov Test
    ks_stat, ks_pvalue = ks_2samp(reference, current)
    results['ks'] = {
        'statistic': ks_stat,
        'pvalue': ks_pvalue,
        'drift': ks_pvalue < threshold
    }
    
    # Wasserstein Distance (Earth Mover's Distance)
    w_distance = wasserstein_distance(reference, current)
    results['wasserstein'] = {
        'distance': w_distance,
        'drift': w_distance > 0.1  # Threshold depends on domain
    }
    
    # Population Stability Index (PSI)
    def calculate_psi(reference, current, buckets=10):
        # Break into buckets
        breakpoints = np.linspace(
            min(min(reference), min(current)),
            max(max(reference), max(current)),
            buckets + 1
        )
        
        reference_counts = np.histogram(reference, breakpoints)[0]
        current_counts = np.histogram(current, breakpoints)[0]
        
        # Convert to proportions
        reference_prop = reference_counts / len(reference)
        current_prop = current_counts / len(current)
        
        # Replace zeros with small value
        reference_prop = np.where(reference_prop == 0, 0.0001, reference_prop)
        current_prop = np.where(current_prop == 0, 0.0001, current_prop)
        
        # Calculate PSI
        psi = np.sum((current_prop - reference_prop) * np.log(current_prop / reference_prop))
        return psi
    
    psi = calculate_psi(reference, current)
    results['psi'] = {
        'value': psi,
        'drift': psi > 0.25  # PSI > 0.25 indicates significant drift
    }
    
    return results
# Detect drift
drift_results = detect_drift(reference_feature, current_feature)
print("Drift Detection Results:")
for test, result in drift_results.items():
    print(f"{test}: {result}")
# Overall drift decision
any_drift = any(result['drift'] for result in drift_results.values())
print(f"\nOverall: {'DRIFT DETECTED' if any_drift else 'No drift detected'}")
```
::::

::::{dropdown} Simple Monitoring Dashboard
```python
import streamlit as st
import pandas as pd
import plotly.express as px
from datetime import datetime, timedelta
# Set page config
st.set_page_config(page_title="Model Monitoring Dashboard", layout="wide")
# Load monitoring data (in production, this would come from a database)
@st.cache_data(ttl=300)  # Cache for 5 minutes
def load_monitoring_data():
    # Simulate monitoring data
    dates = pd.date_range(start=datetime.now() - timedelta(days=30), end=datetime.now(), freq='H')
    
    data = {
        'timestamp': dates,
        'latency_ms': np.random.normal(100, 20, len(dates)).clip(50, 500),
        'error_rate': np.random.beta(2, 100, len(dates)) * 0.1,
        'prediction_count': np.random.poisson(100, len(dates)),
        'accuracy': np.random.normal(0.95, 0.02, len(dates)).clip(0.8, 1.0),
    }
    
    # Add some anomalies
    data['latency_ms'][100:110] = np.random.normal(300, 50, 10).clip(200, 500)
    data['error_rate'][200:210] = np.random.beta(10, 2, 10) * 0.5
    data['accuracy'][300:310] = np.random.normal(0.85, 0.02, 10).clip(0.8, 0.9)
    
    return pd.DataFrame(data)
df = load_monitoring_data()
# Title
st.title("📊 Model Monitoring Dashboard")
# Metrics row
col1, col2, col3, col4 = st.columns(4)
with col1:
    st.metric("Current Accuracy", f"{df['accuracy'].iloc[-1]:.2%}")
with col2:
    st.metric("Avg Latency", f"{df['latency_ms'].iloc[-1]:.1f} ms")
with col3:
    st.metric("Error Rate", f"{df['error_rate'].iloc[-1]:.2%}")
with col4:
    st.metric("Predictions (24h)", f"{df['prediction_count'].iloc[-24:].sum()}")
# Charts
st.subheader("Performance Metrics")
col1, col2 = st.columns(2)
with col1:
    # Latency over time
    fig_latency = px.line(
        df,
        x='timestamp',
        y='latency_ms',
        title='Prediction Latency',
        labels={'latency_ms': 'Latency (ms)', 'timestamp': 'Time'}
    )
    fig_latency.add_hline(y=200, line_dash="dash", line_color="red", annotation_text="Threshold")
    st.plotly_chart(fig_latency, use_container_width=True)
with col2:
    # Accuracy over time
    fig_accuracy = px.line(
        df,
        x='timestamp',
        y='accuracy',
        title='Model Accuracy',
        labels={'accuracy': 'Accuracy', 'timestamp': 'Time'}
    )
    fig_accuracy.add_hline(y=0.9, line_dash="dash", line_color="red", annotation_text="Threshold")
    st.plotly_chart(fig_accuracy, use_container_width=True)
col1, col2 = st.columns(2)
with col1:
    # Error rate over time
    fig_errors = px.line(
        df,
        x='timestamp',
        y='error_rate',
        title='Error Rate',
        labels={'error_rate': 'Error Rate', 'timestamp': 'Time'}
    )
    fig_errors.add_hline(y=0.1, line_dash="dash", line_color="red", annotation_text="Threshold")
    st.plotly_chart(fig_errors, use_container_width=True)
with col2:
    # Prediction count over time
    fig_count = px.bar(
        df,
        x='timestamp',
        y='prediction_count',
        title='Prediction Count',
        labels={'prediction_count': 'Count', 'timestamp': 'Time'}
    )
    st.plotly_chart(fig_count, use_container_width=True)
# Alerts
st.subheader("🚨 Alerts")
# Check for anomalies
alerts = []
if df['latency_ms'].iloc[-1] > 200:
    alerts.append(f"⚠️ High latency: {df['latency_ms'].iloc[-1]:.1f} ms")
if df['error_rate'].iloc[-1] > 0.1:
    alerts.append(f"⚠️ High error rate: {df['error_rate'].iloc[-1]:.2%}")
if df['accuracy'].iloc[-1] < 0.9:
    alerts.append(f"⚠️ Low accuracy: {df['accuracy'].iloc[-1]:.2%}")
if alerts:
    for alert in alerts:
        st.error(alert)
else:
    st.success("✅ All systems normal")
```
::::

## Foundation Models & LLMOps
### Learning Objectives
- **Know**: What foundation models are and which ones matter today
- **Know**: Difference between standard and reasoning models
- **Know**: Test-time compute as a new scaling axis
- **Know**: In-context learning, few-shot prompting, and prompt engineering
- **Familiar**: How LLMs are deployed in production (LLMOps)
- **Familiar**: Main challenges of running LLMs in production
- **Familiar**: Techniques to adapt and ground LLMs (fine-tuning, RAG, agents)
### Key Concepts
#### Foundation Models
```{list-table}
:header: Model, Organization, Size, Key Features
:widths: 20 20 10 50
* - **GPT-5**
  - OpenAI
  - ~175B+
  - Most advanced, multimodal capabilities
* - **Claude 3**
  - Anthropic
  - ~100B-200B
  - Strong reasoning, vision capabilities
* - **Gemini**
  - Google
  - ~100B-200B
  - Multimodal, integrated with Google ecosystem
* - **LLaMA 3**
  - Meta
  - 8B-70B
  - Open weights, strong performance
* - **Mistral**
  - Mistral AI
  - 8B-80B
  - Open weights, efficient architecture
* - **DeepSeek**
  - DeepSeek
  - ~670B
  - Reasoning-focused, long context
```
#### Reasoning vs Standard Models
- **Standard Models**: Generate responses directly
- **Reasoning Models**: Use chain-of-thought, show intermediate steps
  - *Test-Time Compute*: More compute during inference for better reasoning
  - *Examples*: Claude 3, GPT-4 with chain-of-thought
#### Prompt Engineering
- **Zero-Shot**: No examples provided
- **Few-Shot**: Provide examples in the prompt
- **Chain-of-Thought**: Show reasoning steps
- **Self-Consistency**: Sample multiple times, select most consistent
- **Tree-of-Thoughts**: Explore multiple reasoning paths
#### LLMOps Challenges
1. **Hallucinations**: Models generate false information
2. **Bias**: Models reflect biases in training data
3. **Non-determinism**: Same prompt can produce different outputs
4. **Latency**: Large models are slow
5. **Cost**: API calls and compute are expensive
6. **Security**: Prompt injection, data leakage
7. **Evaluation**: Hard to measure quality
#### LLM Adaptation Techniques
1. **Fine-Tuning**: Update model weights on domain-specific data
   - *Full Fine-Tuning*: Update all weights
   - *LoRA*: Low-Rank Adaptation (efficient)
   - *QLoRA*: Quantized LoRA
2. **Retrieval-Augmented Generation (RAG)**:
   - Retrieve relevant documents
   - Provide as context to LLM
   - Reduces hallucinations, improves factual accuracy
3. **Agents and Tool Use**:
   - LLM can call external tools/APIs
   - Multi-step reasoning and action
   - Examples: LangChain, AutoGen
4. **Model Context Protocol (MCP)**:
   - Standard for connecting LLMs to data sources
   - Pluggable architecture

### Code Examples

::::{dropdown} Prompt Engineering with LangChain
```python
from langchain_core.prompts import ChatPromptTemplate, HumanMessagePromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_community.llms import HuggingFaceHub
import os
# Set Hugging Face API token
os.environ["HUGGINGFACEHUB_API_TOKEN"] = "your_api_token"
# Initialize LLM
llm = HuggingFaceHub(
    repo_id="google/flan-t5-xxl",
    model_kwargs={"temperature": 0.5, "max_length": 512}
)
# Simple prompt
simple_prompt = ChatPromptTemplate.from_template("Tell me about {topic}")
simple_chain = simple_prompt | llm | StrOutputParser()
# Few-shot prompt
few_shot_template = """Answer the following questions based on the examples below.
Example 1:
Question: What is the capital of France?
Answer: The capital of France is Paris.
Example 2:
Question: What is the capital of Germany?
Answer: The capital of Germany is Berlin.
Now answer this question:
Question: {question}
Answer: """
few_shot_prompt = ChatPromptTemplate.from_template(few_shot_template)
few_shot_chain = few_shot_prompt | llm | StrOutputParser()
# Chain-of-thought prompt
cot_template = """Let's think step by step to solve this problem.
Problem: {problem}
Step 1: Understand the problem
{step1}
Step 2: Break it down
{step2}
Step 3: Solve each part
{step3}
Final Answer: """
cot_prompt = ChatPromptTemplate.from_template(cot_template)
cot_chain = cot_prompt | llm | StrOutputParser()
# Use the chains
print("Simple prompt:")
print(simple_chain.invoke({"topic": "machine learning"}))
print("\nFew-shot prompt:")
print(few_shot_chain.invoke({"question": "What is the capital of Italy?"}))
print("\nChain-of-thought prompt:")
print(cot_chain.invoke({
    "problem": "What is 25 * 4?",
    "step1": "We need to multiply 25 by 4.",
    "step2": "This is a simple multiplication problem.",
    "step3": "25 * 4 = 100"
}))
```
::::

::::{dropdown} RAG with LangChain
```python
from langchain_community.document_loaders import WebBaseLoader
from langchain_community.vectorstores import FAISS
from langchain_community.embeddings import HuggingFaceEmbeddings
from langchain_text_splitters import RecursiveCharacterTextSplitter
from langchain_core.prompts import ChatPromptTemplate
from langchain_community.llms import HuggingFaceHub
from langchain.chains import RetrievalQA
# Load documents
loader = WebBaseLoader([
    "https://en.wikipedia.org/wiki/Machine_learning",
    "https://en.wikipedia.org/wiki/Deep_learning"
])
docs = loader.load()
# Split documents
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200
)
splits = text_splitter.split_documents(docs)
# Create embeddings
embedding = HuggingFaceEmbeddings(model_name="sentence-transformers/all-mpnet-base-v2")
# Create vector store
vectorstore = FAISS.from_documents(documents=splits, embedding=embedding)
# Create retriever
retriever = vectorstore.as_retriever()
# Initialize LLM
llm = HuggingFaceHub(
    repo_id="google/flan-t5-xxl",
    model_kwargs={"temperature": 0.5, "max_length": 512}
)
# Create RAG chain
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True
)
# Ask a question
question = "What is the difference between machine learning and deep learning?"
result = qa_chain.invoke({"query": question})
print(f"Question: {question}")
print(f"\nAnswer: {result['result']}")
print(f"\nSource documents:")
for doc in result['source_documents']:
    print(f"- {doc.metadata['source']}")
```
::::

::::{dropdown} LoRA Fine-Tuning
```python
from transformers import AutoModelForCausalLM, AutoTokenizer, TrainingArguments
from peft import LoraConfig, get_peft_model, prepare_model_for_kbit_training
from datasets import load_dataset
import torch
from trl import SFTTrainer
# Load base model and tokenizer
model_name = "mistralai/Mistral-7B-v0.1"
tokenizer = AutoTokenizer.from_pretrained(model_name)
tokenizer.pad_token = tokenizer.eos_token
# Load model in 4-bit quantization
model = AutoModelForCausalLM.from_pretrained(
    model_name,
    load_in_4bit=True,
    device_map="auto"
)
# Prepare model for training
model = prepare_model_for_kbit_training(model)
# Define LoRA config
peft_config = LoraConfig(
    r=16,  # Rank
    lora_alpha=32,
    lora_dropout=0.05,
    bias="none",
    task_type="CAUSAL_LM",
    target_modules=["q_proj", "k_proj", "v_proj", "o_proj"]  # Target layers
)
# Add LoRA adapters
model = get_peft_model(model, peft_config)
# Load dataset
dataset = load_dataset("timdettmers/openassistant-guanaco")
train_dataset = dataset["train"].select(range(1000))  # Use subset for demo
# Training arguments
training_args = TrainingArguments(
    output_dir="./results",
    per_device_train_batch_size=4,
    gradient_accumulation_steps=4,
    learning_rate=2e-4,
    num_train_epochs=3,
    logging_steps=10,
    save_strategy="epoch",
    report_to="none"
)
# Create trainer
trainer = SFTTrainer(
    model=model,
    args=training_args,
    train_dataset=train_dataset,
    dataset_text_field="text",
    max_seq_length=512,
    tokenizer=tokenizer,
    packing=True
)
# Train
trainer.train()
# Save model
trainer.model.save_pretrained("./lora_model")
tokenizer.save_pretrained("./lora_model")
# Inference with LoRA
from peft import PeftModel
# Load base model
base_model = AutoModelForCausalLM.from_pretrained(
    model_name,
    load_in_4bit=True,
    device_map="auto"
)
# Load LoRA adapter
model = PeftModel.from_pretrained(base_model, "./lora_model")
# Generate text
input_text = "What is machine learning?"
inputs = tokenizer(input_text, return_tensors="pt").to("cuda")
outputs = model.generate(**inputs, max_new_tokens=100)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```
::::

## Cloud Platforms
### Learning Objectives
- **Know**: Key components in a cloud-based MLOps pipeline
- **Familiar**: Typical workflow and key practices for cloud MLOps
- **Familiar**: Considerations for deploying ML models to cloud
- **Apply**: Design and deploy end-to-end MLOps pipeline using Vertex AI
- **Apply**: Orchestrate ML workflows using Kubeflow Pipelines
- **Apply**: Set up model deployment and prediction endpoints
### Key Concepts
#### Cloud Deployment Models
```{list-table}
:header: Model, Description, Examples
:widths: 15 50 35
* - **Public Cloud**
  - Services offered over public internet
  - AWS, GCP, Azure
* - **Private Cloud**
  - Dedicated infrastructure for single organization
  - OpenStack, VMware
* - **Hybrid Cloud**
  - Combination of public and private
  - AWS Outposts, Azure Arc
* - **Sovereign Cloud**
  - Cloud within specific jurisdiction
  - Government clouds
```
#### Cloud Service Models
```{list-table}
:header: Model, Description, Responsibility
:widths: 15 40 45
* - **IaaS**
  - Infrastructure as a Service
  - User: OS, middleware, apps, data
* - **PaaS**
  - Platform as a Service
  - User: Apps, data
* - **SaaS**
  - Software as a Service
  - User: Data
* - **Serverless**
  - Event-driven, auto-scaling
  - User: Code
```
#### Vertex AI Components
1. **Vertex AI Workbench**: JupyterLab environments
2. **Vertex AI Training**: Managed training service
3. **Vertex AI Prediction**: Model serving
4. **Vertex AI Pipelines**: Workflow orchestration
5. **Vertex AI Model Registry**: Model versioning
6. **Vertex AI Feature Store**: Feature management
7. **Vertex AI Monitoring**: Model monitoring
#### Cloud MLOps Pipeline
```{mermaid}
:align: center
flowchart LR
    A[Data Ingestion] --> B[Data Storage]
    B --> C[Data Processing]
    C --> D[Feature Engineering]
    D --> E[Model Training]
    E --> F[Model Evaluation]
    F --> G[Model Registry]
    G --> H[Model Deployment]
    H --> I[Model Serving]
    I --> J[Monitoring]
    J -->|Feedback| A
    J -->|Retraining| E
```
### Code Examples

::::{dropdown} Vertex AI Training
```python
from google.cloud import aiplatform
from google.cloud.aiplatform import hyperparameter_tuning as hpt
# Initialize Vertex AI
aiplatform.init(project="your-project-id", location="us-central1")
# Define custom training job
def train_model():
    # This would be your training script
    # In practice, this runs in a container on Vertex AI
    import argparse
    import torch
    from transformers import Trainer, TrainingArguments
    
    parser = argparse.ArgumentParser()
    parser.add_argument("--learning_rate", type=float, default=2e-5)
    parser.add_argument("--batch_size", type=int, default=32)
    parser.add_argument("--epochs", type=int, default=3)
    args = parser.parse_args()
    
    # Your training code here
    print(f"Training with LR={args.learning_rate}, BS={args.batch_size}, Epochs={args.epochs}")
# Create custom container training job
job = aiplatform.CustomTrainingJob(
    display_name="fashion-mnist-training",
    script_path="train.py",
    container_uri="gcr.io/cloud-aiplatform/training/pytorch-gpu.2-8",
    requirements=["torch", "transformers"],
    model_serving_container_image_uri="gcr.io/cloud-aiplatform/prediction/pytorch-gpu.2-8"
)
# Run training job
model = job.run(
    machine_type="n1-standard-4",
    accelerator_type="NVIDIA_TESLA_T4",
    accelerator_count=1,
    replica_count=1,
    args=[
        f"--learning_rate={0.001}",
        f"--batch_size={32}",
        f"--epochs={3}"
    ]
)
# Wait for job to complete
model.wait()
print(f"Training completed. Model: {model.resource_name}")
```
::::

::::{dropdown} Vertex AI Hyperparameter Tuning
```python
from google.cloud import aiplatform
from google.cloud.aiplatform import hyperparameter_tuning as hpt
# Initialize Vertex AI
aiplatform.init(project="your-project-id", location="us-central1")
# Define hyperparameter tuning job
hp_job = aiplatform.HyperparameterTuningJob(
    display_name="fashion-mnist-hpo",
    custom_job=aiplatform.CustomTrainingJob.from_local_script(
        display_name="fashion-mnist-train",
        script_path="train.py",
        container_uri="gcr.io/cloud-aiplatform/training/pytorch-gpu.2-8",
        requirements=["torch", "transformers"],
    ),
    metric_spec={
        "val_accuracy": "maximize"
    },
    parameter_spec={
        "learning_rate": hpt.DoubleParameterSpec(
            min=1e-5, max=1e-3, scale="log"
        ),
        "batch_size": hpt.DiscreteParameterSpec(
            values=[16, 32, 64, 128], scale="linear"
        ),
        "epochs": hpt.IntegerParameterSpec(
            min=1, max=5, scale="linear"
        )
    },
    max_trial_count=20,
    parallel_trial_count=4
)
# Run hyperparameter tuning
hp_job.run(
    machine_type="n1-standard-4",
    accelerator_type="NVIDIA_TESLA_T4",
    accelerator_count=1
)
# Wait for job to complete
hp_job.wait()
# Get best trial
best_trial = hp_job.get_best_trial()
print(f"Best hyperparameters: {best_trial.hyperparameters}")
print(f"Best validation accuracy: {best_trial.final_measurement.metrics['val_accuracy']}")
```
::::

::::{dropdown} Vertex AI Pipeline
```python
from google.cloud import aiplatform
from kfp.v2 import compiler
from kfp.v2.dsl import component, pipeline, Input, Output, Model
# Define pipeline components
@component(
    packages_to_install=["pandas", "scikit-learn"],
    output_component_file="preprocess_component.yaml"
)
def preprocess_data(
    input_data: Input[Artifact],
    output_data: Output[Artifact]
):
    import pandas as pd
    from sklearn.model_selection import train_test_split
    
    # Load data
    df = pd.read_csv(input_data.path)
    
    # Preprocessing
    # ... your preprocessing code ...
    
    # Save processed data
    train, test = train_test_split(df, test_size=0.2)
    train.to_csv(f"{output_data.path}/train.csv", index=False)
    test.to_csv(f"{output_data.path}/test.csv", index=False)
@component(
    packages_to_install=["torch", "transformers"],
    output_component_file="train_component.yaml"
)
def train_model(
    train_data: Input[Artifact],
    model: Output[Model]
):
    import torch
    from transformers import AutoModelForSequenceClassification, Trainer, TrainingArguments
    
    # Load data
    train_df = pd.read_csv(train_data.path + "/train.csv")
    
    # Train model
    # ... your training code ...
    
    # Save model
    model.save_pretrained(model.path)
@component(
    packages_to_install=["torch", "transformers"],
    output_component_file="deploy_component.yaml"
)
def deploy_model(
    model: Input[Model],
    endpoint_name: str
):
    from google.cloud import aiplatform
    
    # Upload model to Vertex AI
    aiplatform.Model.upload(
        display_name="fashion-mnist-model",
        artifact_uri=model.uri,
        serving_container_image_uri="gcr.io/cloud-aiplatform/prediction/pytorch-gpu.2-8"
    )
    
    # Create endpoint
    endpoint = aiplatform.Endpoint.create(display_name=endpoint_name)
    
    # Deploy model
    model.deploy(
        endpoint=endpoint,
        machine_type="n1-standard-2",
        min_replica_count=1,
        max_replica_count=3
    )
# Define pipeline
@pipeline(
    name="fashion-mnist-pipeline",
    pipeline_root="gs://your-bucket/pipelines"
)
def fashion_mnist_pipeline(
    input_data: str = "gs://your-bucket/data/raw/dataset.csv",
    endpoint_name: str = "fashion-mnist-endpoint"
):
    # Preprocess data
    preprocess_task = preprocess_data(input_data=input_data)
    
    # Train model
    train_task = train_model(train_data=preprocess_task.output)
    
    # Deploy model
    deploy_task = deploy_model(
        model=train_task.output,
        endpoint_name=endpoint_name
    )
# Compile pipeline
compiler.Compiler().compile(
    pipeline_func=fashion_mnist_pipeline,
    package_path="pipeline.json"
)
# Submit pipeline to Vertex AI
aiplatform.PipelineJob(
    display_name="fashion-mnist-pipeline-job",
    template_path="pipeline.json",
    parameter_values={
        "input_data": "gs://your-bucket/data/raw/dataset.csv",
        "endpoint_name": "fashion-mnist-endpoint"
    }
).run()
```
::::

::::{dropdown} Vertex AI Endpoint Deployment
```python
from google.cloud import aiplatform
# Initialize Vertex AI
aiplatform.init(project="your-project-id", location="us-central1")
# Upload model
model = aiplatform.Model.upload(
    display_name="text-classification-model",
    artifact_uri="gs://your-bucket/models/text-classification",
    serving_container_image_uri="gcr.io/cloud-aiplatform/prediction/pytorch-gpu.2-8"
)
# Create endpoint
endpoint = aiplatform.Endpoint.create(
    display_name="text-classification-endpoint"
)
# Deploy model to endpoint
deployed_model = model.deploy(
    endpoint=endpoint,
    machine_type="n1-standard-4",
    accelerator_type="NVIDIA_TESLA_T4",
    accelerator_count=1,
    min_replica_count=1,
    max_replica_count=3,
    traffic_split={"0": 100}  # 100% traffic to this model
)
print(f"Model deployed to endpoint: {endpoint.resource_name}")
# Make prediction
text = "This is a sample text to classify."
prediction = deployed_model.predict(instances=[{"text": text}])
print(f"Prediction: {prediction}")
# Get prediction from endpoint directly
endpoint_prediction = endpoint.predict(instances=[{"text": text}])
print(f"Endpoint prediction: {endpoint_prediction}")
# Monitor endpoint
# Get metrics
metrics = endpoint.gcp_resources[0].list_model_deployment_monitoring_jobs()
print(f"Monitoring jobs: {metrics}")
# Get traffic and logs
logs = endpoint.list_model_deployment_logs()
for log in logs:
    print(f"Log: {log}")
```
::::

## ML Product Management, Roles & Teams
### Learning Objectives
- **Know**: How AI-driven prediction impacts business strategy and decision-making
- **Know**: Key factors in assessing feasibility and strategic value of ML projects
- **Familiar**: Main ML roles and their responsibilities
- **Familiar**: Different organizational models for structuring ML efforts
- **Familiar**: How organizational models relate to ML maturity levels
- **Apply**: Identify suitable ML roles for a business case
- **Apply**: Evaluate and recommend appropriate ML team structure
### Key Concepts
#### ML Roles
```{list-table}
:header: Role, Responsibilities, Skills
:widths: 20 50 30
* - **Data Engineer**
  - Build and maintain data infrastructure, ETL pipelines
  - SQL, Python, Spark, Airflow
* - **ML Engineer**
  - Develop ML models, implement algorithms, deploy models
  - Python, ML frameworks, software engineering
* - **ML Researcher**
  - Develop new algorithms, publish papers
  - Research, mathematics, ML theory
* - **ML Product Manager**
  - Define ML product vision, align with business goals
  - Product management, business acumen
* - **Data Scientist**
  - Exploratory analysis, model prototyping, insights
  - Statistics, Python, visualization
* - **MLOps Engineer**
  - Implement MLOps practices, CI/CD, monitoring
  - DevOps, ML, infrastructure
* - **AI/LLM Engineer**
  - Specialized in LLM development and deployment
  - LLMs, prompt engineering, fine-tuning
```
#### Organizational Models
```{list-table}
:header: Model, Description, Pros, Cons
:widths: 15 30 25 25
* - **Centralized**
  - Single central ML team serves entire organization
  - Economies of scale, expertise concentration
  - Bottleneck, less domain knowledge
* - **Decentralized**
  - ML teams embedded in business units
  - Close to domain, faster iteration
  - Duplication, less sharing
* - **Hybrid**
  - Central platform team + embedded teams
  - Balance of sharing and domain knowledge
  - More complex coordination
```
#### ML Maturity Levels
```{list-table}
:header: Level, Description, Characteristics
:widths: 15 40 45
* - **Nascent**
  - Exploring ML, no production systems
  - Ad-hoc projects, limited infrastructure
* - **Emerging**
  - First ML systems in production
  - Basic MLOps, some automation
* - **Maturing**
  - Multiple ML systems, standardized processes
  - Full MLOps, monitoring, retraining
* - **ML-First**
  - ML is core to business, competitive advantage
  - Advanced MLOps, continuous improvement
```
#### ML vs Business Objectives
- **ML Objectives**: Accuracy, latency, throughput, model size
- **Business Objectives**: ROI, cost reduction, revenue growth, compliance
- **Alignment**: ML objectives should directly support business objectives
- **Success Criteria**: Define measurable criteria for both ML and business metrics
### Organizational Examples

::::{dropdown} Team Structure Decision Tree
```python
class MLTeamStructure:
    """
    Helper class to determine appropriate ML team structure
    based on organizational characteristics.
    """
    
    def __init__(self, org_size, ml_maturity, domain_complexity, budget):
        self.org_size = org_size  # small, medium, large
        self.ml_maturity = ml_maturity  # nascent, emerging, maturing, ml_first
        self.domain_complexity = domain_complexity  # low, medium, high
        self.budget = budget  # low, medium, high
    
    def recommend_structure(self):
        """Recommend team structure based on organizational characteristics."""
        
        if self.org_size == "small" or self.ml_maturity == "nascent":
            return {
                "structure": "Centralized",
                "reason": "Small organizations or those new to ML benefit from centralized expertise"
            }
        
        if self.domain_complexity == "high" and self.org_size == "large":
            return {
                "structure": "Decentralized",
                "reason": "Large organizations with complex domains need embedded ML teams"
            }
        
        if self.ml_maturity in ["emerging", "maturing"]:
            return {
                "structure": "Hybrid",
                "reason": "Most organizations benefit from a hybrid approach"
            }
        
        if self.ml_maturity == "ml_first" and self.budget == "high":
            return {
                "structure": "Centralized Platform + Decentralized",
                "reason": "ML-first organizations need both platform and domain expertise"
            }
        
        return {
            "structure": "Hybrid",
            "reason": "Default recommendation for most organizations"
        }
    
    def recommend_roles(self, project_type):
        """Recommend roles for a specific project type."""
        
        base_roles = ["ML Engineer", "Data Engineer", "ML Product Manager"]
        
        if project_type == "research":
            return base_roles + ["ML Researcher"]
        
        if project_type == "llm":
            return base_roles + ["AI/LLM Engineer", "Data Scientist"]
        
        if project_type == "data_intensive":
            return base_roles + ["Data Scientist", "Data Engineer"]
        
        if project_type == "production":
            return base_roles + ["MLOps Engineer", "DevOps Engineer"]
        
        return base_roles
# Example usage
org = MLTeamStructure(
    org_size="large",
    ml_maturity="maturing",
    domain_complexity="high",
    budget="high"
)
structure = org.recommend_structure()
print(f"Recommended structure: {structure['structure']}")
print(f"Reason: {structure['reason']}")
roles = org.recommend_roles("llm")
print(f"Recommended roles for LLM project: {', '.join(roles)}")
```
::::

::::{dropdown} ML Project Feasibility Assessment
```python
class MLProjectAssessment:
    """
    Framework for assessing ML project feasibility and strategic value.
    """
    
    def __init__(self, project_name):
        self.project_name = project_name
        self.scores = {}
    
    def assess_feasibility(self, data_availability, technical_feasibility, resource_availability):
        """
        Assess project feasibility on a scale of 1-10.
        
        Args:
            data_availability: 1-10 (availability and quality of data)
            technical_feasibility: 1-10 (technical complexity)
            resource_availability: 1-10 (available resources)
        """
        feasibility_score = (data_availability * 0.4 + 
                            technical_feasibility * 0.3 + 
                            resource_availability * 0.3)
        self.scores['feasibility'] = feasibility_score
        return feasibility_score
    
    def assess_strategic_value(self, business_impact, alignment, roi_potential):
        """
        Assess strategic value on a scale of 1-10.
        
        Args:
            business_impact: 1-10 (potential business impact)
            alignment: 1-10 (alignment with business strategy)
            roi_potential: 1-10 (potential return on investment)
        """
        strategic_score = (business_impact * 0.4 + 
                          alignment * 0.3 + 
                          roi_potential * 0.3)
        self.scores['strategic_value'] = strategic_score
        return strategic_score
    
    def get_recommendation(self):
        """Get recommendation based on assessment scores."""
        if not self.scores:
            return "Please assess feasibility and strategic value first."
        
        feasibility = self.scores.get('feasibility', 0)
        strategic_value = self.scores.get('strategic_value', 0)
        
        if feasibility >= 8 and strategic_value >= 8:
            return "✅ HIGH PRIORITY: Strong feasibility and strategic value. Proceed with project."
        
        if feasibility >= 8 and strategic_value >= 5:
            return "✅ RECOMMENDED: Good feasibility. Consider strategic alignment."
        
        if strategic_value >= 8 and feasibility >= 5:
            return "⚠️ CONDITIONAL: High strategic value but feasibility concerns. Invest in feasibility improvement."
        
        if feasibility >= 5 and strategic_value >= 5:
            return "🟡 MODERATE: Acceptable scores. Proceed with caution."
        
        return "❌ NOT RECOMMENDED: Low scores. Re-evaluate project."
    
    def get_ml_objectives(self, business_objective):
        """
        Translate business objectives to ML objectives.
        
        Args:
            business_objective: Business goal (e.g., "increase sales", "reduce costs")
            
        Returns:
            dict: ML objectives that support the business objective
        """
        ml_objectives = {
            "increase sales": {
                "primary": "maximize conversion rate",
                "secondary": ["minimize false positives", "maximize precision"],
                "metrics": ["conversion_rate", "precision", "recall", "F1"]
            },
            "reduce costs": {
                "primary": "minimize operational costs",
                "secondary": ["maximize automation", "minimize manual review"],
                "metrics": ["cost_per_prediction", "automation_rate", "accuracy"]
            },
            "improve customer satisfaction": {
                "primary": "maximize customer satisfaction score",
                "secondary": ["minimize response time", "maximize personalization"],
                "metrics": ["csat_score", "response_latency", "personalization_score"]
            },
            "ensure compliance": {
                "primary": "maximize compliance score",
                "secondary": ["minimize false negatives", "maximize explainability"],
                "metrics": ["compliance_score", "false_negative_rate", "explainability_score"]
            }
        }
        
        return ml_objectives.get(business_objective, {
            "primary": "define custom objective",
            "secondary": [],
            "metrics": []
        })
# Example usage
assessment = MLProjectAssessment("Customer Churn Prediction")
# Assess feasibility
feasibility = assessment.assess_feasibility(
    data_availability=9,
    technical_feasibility=8,
    resource_availability=7
)
# Assess strategic value
strategic_value = assessment.assess_strategic_value(
    business_impact=8,
    alignment=9,
    roi_potential=7
)
print(f"Project: {assessment.project_name}")
print(f"Feasibility Score: {feasibility:.1f}/10")
print(f"Strategic Value Score: {strategic_value:.1f}/10")
print(f"\nRecommendation: {assessment.get_recommendation()}")
# Get ML objectives
business_obj = "increase sales"
ml_obj = assessment.get_ml_objectives(business_obj)
print(f"\nML Objectives for '{business_obj}':")
print(f"Primary: {ml_obj['primary']}")
print(f"Secondary: {', '.join(ml_obj['secondary'])}")
print(f"Metrics: {', '.join(ml_obj['metrics'])}")
```
::::
