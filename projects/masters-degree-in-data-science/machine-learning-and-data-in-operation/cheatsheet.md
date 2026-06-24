---
title: Cheatsheet - MLOps
author: ''
exports:
- format: pdf
  template: arxiv_two_column
  output: MLOps-Cheatsheet.pdf
  id: mlops-cheatsheet-pdf
downloads:
  - id: mlops-cheatsheet-pdf
    title: Download as PDF
---

## MLOps Fundamentals

- **MLOps:**: (1) Extension of DevOps to ML projects; (2) Tools & best practices for bringing ML into production; (3) Systems approach to ML
- **ML Engineering:** 90% engineering, 10% ML
- **ML is systems engineering:** Focus on reliability, not just accuracy
- **Data quality > Model complexity:** Garbage in, garbage out
- **Monitor everything:** Data drift, model drift, performance
- **Iterate continuously:** ML is never "set and forget"
- **Align with business:** Technical success $\neq$ business success

| ML Product Archetype                   | Definition                                                                           | Example                               | Key Question                                      |
| ---------------------- |--------------------------------------------------------------------------------------| ------------------------------------- | ------------------------------------------------- |
| **Software 2.0**       | Take something  traditional SW is good at and make it better with ML | Code completion, recommendations      | Does ML truly improve performance/business value? |
| **Human in the Loop**  | Help humans do their  job better by complementing them with ML based tools                                                             | Email autocomplete, Turn sketches into slides | How good must the system be to be useful?         |
| **Autonomous Systems** | Take something humans do today and automate it with ML                                                         | Self-driving, customer support        | What's acceptable failure rate?                   |

**ML Research vs Production**

| Aspect         | Research              | Production                       |
| -------------- | --------------------- | -------------------------------- |
| **Goal**       | Publish novel results | Build reliable, scalable systems |
| **Data**       | Clean, curated        | Messy, real-world                |
| **Evaluation** | Accuracy on test set  | Performance, latency, robustness |
| **Iteration**  | Experimental          | Incremental, controlled          |
| **Focus**      | Model innovation      | System reliability               |

Also important for Production but not so much for Research: Fairness & Interpretability.

**MLOps Components**

**Business Objectives** → **Data Engineering** → **Model Training & Evaluation** → **Model Testing** → **Deployment** → **Monitoring** → (Feedback Loop)

**Data Flywheel**

**More data** → **Better model** → **More users** → **More data** → ...

## Deep Learning Fundamentals

- **Core Concepts**
  - **Forward Pass**: Input → Hidden Layers → Output
  - **Backpropagation**: Compute gradients using chain rule
  - **Gradient Descent**: Update weights: $w = w - \alpha \frac{\partial L}{\partial w}$
  - **Loss Functions**:
    - Regression: **MSE** = $\mathrm{MSE} = \frac{1}{n}\sum_{i=1}^{n} (\hat{y}_i - y_i)^2$
    - Classification: **Cross-Entropy** $= -\sum_{i} y_i \log(\hat{y}_i)$
- **Optimizers**
  - **SGD**: Basic, needs tuning
  - **Adam**: Adaptive learning rates (most popular)
  - **RMSprop**: Adaptive, good for RNNs
- **Regularization**
  - **Dropout**: Randomly deactivate neurons (rate=0.2-0.5)
  - **Weight Decay**: L2 penalty on weights
  - **BatchNorm**: Normalize layer inputs

**Neural Network Architectures**

| Architecture    | Key Idea              | Use Case             | Example              |
| --------------- | --------------------- | -------------------- | -------------------- |
| **CNN**         | Convolution + Pooling | Image classification | ResNet, VGG, AlexNet |
| **Transformer** | Self-attention        | Sequential data      | BERT, ViT            |
| **RNN/LSTM**    | Recurrent connections | Time series, text    | -                    |

**Training Process**
1. Define: Input size, layers, activations (ReLU, Softmax), output, loss, optimizer, metrics
2. Train: Adjust weights via backpropagation to minimize loss
3. Evaluate: Check metrics on validation set

## Data Engineering

| Data Storage Type   | Description           | Use Cases           | Examples            |
|---------------------| --------------------- | ------------------- | ------------------- |
| **Filesystem**      | Local disk storage    | Dev, small datasets | CSV, JSON, Parquet  |
| **Object Storage**  | Distributed, scalable | Large datasets      | S3, GCS, Azure Blob |
| **Databases**       | Structured, queryable | Transactional data  | PostgreSQL, MySQL   |
| **Data Lakes**      | Raw data repositories | Big data, analytics | Delta Lake, Iceberg |
| **Data Warehouses** | Analytics-optimized   | BI                  | BigQuery, Snowflake |

- **Data Processing**
  - **DAG**: Directed Acyclic Graph (tasks = nodes, dependencies = edges)
  - **Workflow Managers**: Airflow (Python), Spark (distributed), Metaflow (AWS), Ploomber (lightweight)
  - **ETL/ELT**: Extract → Transform → Load
- **Feature Stores**
  - **Purpose**: Centralized feature repository
  - **Benefits**: Avoid recomputation, ensure training/serving consistency, share features
  - **Examples**: Feast, Tecton, Hopsworks
- **Data Versioning**
  - **Git LFS**: Large File Storage for Git
  - **DVC**: Data Version Control (like Git for data)
  - **Others**: Delta Lake, lakeFS, Oxen

## Deployment

| Prediction Pattern       | Description                     | Latency    | Use Cases               |
| ------------- | ------------------------------- | ---------- | ----------------------- |
| **Batch**     | Process multiple inputs at once | Hours-days | Offline, large datasets |
| **Online**    | Process one input at a time     | ms-seconds | Real-time apps          |
| **Streaming** | Continuous data processing      | Seconds    | Real-time analytics     |

| Model Serving Approach             | Pros                       | Cons                                    |
| -------------------- | -------------------------- | --------------------------------------- |
| **Model-in-Service** | Reuse infrastructure       | Different languages, resource conflicts |
| **Model-as-Service** | Dependability, scalability | Added latency, complexity               |
| **Batch Prediction** | Simple, low latency        | Stale predictions, limited inputs       |

| Deployment Option                   | Pros                      | Cons                   |
| ------------------------ | ------------------------- | ---------------------- |
| **Cloud (Managed)**      | Fully managed, scalable   | Vendor lock-in, cost   |
| **Cloud (Self-managed)** | Full control, portable    | More work              |
| **On-Premises**          | Control, privacy          | High cost, maintenance |
| **Edge**                 | Low latency, offline      | Limited resources      |
| **Serverless**           | Auto-scaling, pay-per-use | Cold starts            |

**Model Compression**
- **Pruning**: Remove unimportant weights
- **Quantization**: Reduce precision (float32 → int8)
- **Knowledge Distillation**: Train small model on large model's predictions
- **Low-rank Optimization**: Factorize weight matrices

**Serving Frameworks**

**TorchServe** (PyTorch), **TensorFlow Serving**, **Ray Serve**, **vLLM** (LLMs), **MLServer** (framework-agnostic)

## Monitoring & Continual Learning

ML models degrade over time → **Monitoring is essential**

**Types of Distribution Shifts**

| Type                | Definition                          | Example                              |
| ------------------- |-------------------------------------| ------------------------------------ |
| **Covariate Shift** | $P(X)$ changes, $P(Y \| X)$ changes | Different car mileage distribution   |
| **Label Shift**     | $P(Y)$ changes, $P(X \| Y)$ changes | More expensive cars in dataset       |
| **Concept Drift**   | $P(Y \| X)$ changes                 | Mileage → price relationship changes |

- **Monitoring Approaches**
  - **Operational Metrics**: Latency, uptime, GPU usage
  - **ML Metrics**: Accuracy, drift, fairness
  - **Business Metrics**: ROI, sales, cost reduction
- **Drift Detection Methods**
  - **Statistical Tests**: Kolmogorov-Smirnov (KS), KL Divergence
  - **Tools**: Evidently AI, NannyML, DeepChecks, Fiddler, Whylogs, Alibi Detect
- **Retraining Strategies**
  - **Periodic**: Fixed schedule (e.g., weekly)
  - **Event-driven**: Triggered by drift detection
  - **Continual Learning**: Adapt without catastrophic forgetting
- **Safe Deployment**
  - **A/B Testing**: Compare two versions
  - **Canary Release**: Gradual rollout
  - **Shadow Testing**: Run new model alongside old

## ML Product Management & Teams

| ML Role                   | Responsibilities                     |
| ---------------------- | ------------------------------------ |
| **Data Engineer**      | Data pipelines, ETL, infrastructure  |
| **ML Engineer**        | Model development, deployment, MLOps |
| **ML Product Manager** | Business alignment, prioritization   |
| **MLOps Engineer**     | CI/CD, monitoring, infrastructure    |
| **AI/LLM Engineer**    | LLM-specific development             |

| Organizational Model             | Description                 | Pros                  | Cons        |
| ----------------- | --------------------------- | --------------------- | ----------- |
| **Centralized**   | One ML team                 | Efficiency, expertise | Bottleneck  |
| **Decentralized** | ML in each team             | Alignment, speed      | Duplication |
| **Hybrid**        | Central platform + embedded | Balance               | Complexity  |

**ML Maturity Levels**
1. **Nascent**: Exploring ML, no production
2. **Emerging**: First ML systems in production
3. **Maturing**: Multiple ML systems, standardized
4. **ML-First**: ML is core to business

**Business Alignment**
- **ML Objectives**: Accuracy, latency, throughput, model size
- **Business Objectives**: ROI, cost reduction, revenue growth, compliance
- **Key**: ML objectives must directly support business objectives
