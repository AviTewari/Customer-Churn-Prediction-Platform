# **Customer Churn Prediction Platform**

Welcome to the **Customer Churn Prediction Platform** project! This repository demonstrates an **end-to-end machine learning** workflow for predicting customer churn, incorporating best practices in **software engineering**, **DevOps**, and **MLOps**. It is designed for local development first, with a clear path to containerization and cloud deployment.

---

## **Table of Contents**
1. [Project Overview](#project-overview)  
2. [Architecture](#architecture)  
3. [Features](#features)  
4. [Getting Started (Local Development)](#getting-started-local-development)
5. [Training the Model](#training-the-model)
6. [Running Tests](#running-tests)  
7. [Serving the Model (FastAPI)](#serving-the-model-fastapi)  
8. [Docker Usage](#docker-usage)  
9. [CI/CD Pipeline (Future)](#cicd-pipeline-future)  
10. [Cloud Deployment (Future)](#cloud-deployment-future)  
11. [Contributing](#contributing)  
12. [License](#license)  
13. [Acknowledgments](#acknowledgments)

---

## **1. Project Overview**

The **Customer Churn Prediction Platform** aims to predict which customers are likely to stop using a service (churn) based on historical usage data, demographics, and other relevant factors. You can adapt this platform for various domains (telecommunications, streaming services, subscription products, etc.).

Core **objectives**:
- Provide a reproducible **ML pipeline** (data ingestion → preprocessing → model training).
- Demonstrate **local-first** development, with a path to containerization (Docker) and cloud-based deployment (AWS, GCP, Azure).
- Emphasize **DevOps/MLOps** best practices: environment consistency, testing, CI/CD, and monitoring.

---

## **2. Architecture**

A **high-level workflow** for the platform:

1. **Data**: A CSV or database source with historical customer data, stored locally (`data/`) for development.  
2. **Preprocessing & Feature Engineering**: Scripts transform raw data into ML-ready features.  
3. **Model Training**: Uses scikit-learn (or another library) to train a churn prediction model (e.g., Random Forest, XGBoost).  
4. **Model Artifact**: Trained model is saved (e.g., `model.pkl`) for inference.  
5. **Inference/Serving**: A FastAPI (or Flask) service exposes a `/predict` endpoint for real-time churn predictions.  
6. **Docker**: Containerizes the entire application for consistent deployment.  
7. **Deployment (Future)**: Possible integration with AWS ECS/EKS, Docker Hub, or other cloud options.  
8. **Monitoring & Iteration**: Track performance, gather feedback data, and continuously improve the model.

---

## **3. Features**

- **End-to-end pipeline**: From raw data to a production-ready model.  
- **Local development first**: Easy to set up on a macOS or Windows/Linux environment.  
- **Containerization (Docker)**: Ensures environment consistency.  
- **Modular code structure**: Clear separation of concerns (data utils, training, inference).  
- **FastAPI endpoint** for real-time predictions.  
- **Testing** with `pytest` for robust, reliable code.  
- **Scalable** to cloud environments (AWS, GCP, Azure).

---

## **4. Getting Started (Local Development)**

### **Prerequisites**

- **Git** installed  
- **Conda** (Miniconda/Anaconda) or Python 3.9+  
- (Optional) **Docker Desktop** if you plan to use Docker

### **Steps**

1. **Clone** the repository:
   ```bash
   git clone https://github.com/AviTewari/Customer-Churn-Prediction-Platform.git
   cd Customer-Churn-Prediction-Platform
   ```
2. **Create & Activate** a Conda or virtual environment (example with Conda):
   ```bash
   conda create -n churn-env python=3.9
   conda activate churn-env
   ```
3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
   or
   ```bash
   conda install --file requirements.txt
   ```
4. **Check** everything is set up:
   ```bash
   conda list
   # or pip list
   ```

---

## **5. Training the Model**

1. **Prepare** or **place** a small dataset under `data/` (e.g., `telco_churn.csv`).  
2. **Run** the training script:
   ```bash
   python src/train.py
   ```
   - This will:
     - Load the CSV from `data/`  
     - Preprocess the data (e.g., handle missing values, encode categorical features)  
     - Train a machine learning model (e.g., RandomForest)  
     - Save the trained model artifact (e.g., `model.pkl`) in the project directory

---

## **6. Running Tests**

If the project includes automated tests (e.g., `tests/` folder):

```bash
pytest --maxfail=1 --disable-warnings
```

- **Unit Tests** check individual functions (preprocessing, feature engineering).  
- **Integration Tests** validate the entire pipeline (load → train → evaluate).

---

## **7. Serving the Model (FastAPI)**

After training, you can **serve** the model via an API:

1. **Start** the FastAPI server:
   ```bash
   uvicorn src.app:app --host 0.0.0.0 --port 8000
   ```
2. **Access** the interactive docs at [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).  
3. **Test** the `POST /predict` endpoint:
   ```bash
   curl -X POST -H "Content-Type: application/json" \
     -d '{"features": {"MonthlyCharges": 70, "tenure": 12}}' \
     http://127.0.0.1:8000/predict
   ```

---

## **8. Docker Usage**

To ensure a **portable** environment:

1. **Install** Docker Desktop (if not already).  
2. **Build** the Docker image:
   ```bash
   docker build -t churn-app:latest .
   ```
3. **Run** the container:
   ```bash
   docker run -p 8000:8000 churn-app:latest
   ```
4. **Test** as before:
   ```bash
   curl -X POST -H "Content-Type: application/json" \
     -d '{"features": {"MonthlyCharges": 70, "tenure": 12}}' \
     http://127.0.0.1:8000/predict
   ```

---

## **9. CI/CD Pipeline (Future)**

- **GitHub Actions** or **GitLab CI**: Automate testing, building Docker images, and pushing to a container registry.  
- **Branch Protection Rules**: Ensure code reviews and passing tests before merging to the main branch.  
- **Automated Deployments**: On each merge or tagged release, automatically deploy to staging/production in the cloud.

---

## **10. Cloud Deployment (Future)**

- **AWS ECS or EKS**: Container orchestration for your Docker image.  
- **AWS ECR** or **Docker Hub**: Store images for production usage.  
- **Terraform** or **CloudFormation**: Infrastructure-as-Code to define ECS tasks, load balancers, and networking.  
- **Monitoring & Logging**: Use CloudWatch or equivalent to track logs, performance, and potential data drift.

---

## **11. Contributing**

We welcome contributions! To contribute:

1. **Fork** the repo or create a new branch if you’re a collaborator.  
2. **Commit** changes to your branch (`git checkout -b my-new-feature`).  
3. **Push** to GitHub and open a **Pull Request**.  
4. **Discuss** and **review** your PR. Once approved, changes will be merged into `main`.

---

## **12. License**

This project is released under the **MIT License** (or whichever license you’re using). See the [LICENSE](LICENSE) file for details.

---

## **13. Acknowledgments**

- **Contributors**: [Avi Tewari](https://github.com/AviTewari) and [Harshil Bhandari](https://github.com/Harshil7875).  
- **Resources & Libraries**:  
  - [scikit-learn](https://scikit-learn.org/), [FastAPI](https://fastapi.tiangolo.com/), [pandas](https://pandas.pydata.org/), [Docker](https://www.docker.com/).  
  - [Public Telco Customer Churn dataset](https://www.kaggle.com/blastchar/telco-customer-churn) (if used).  

---

**Thank you for using the Customer Churn Prediction Platform!**  
If you have questions or suggestions, please open an [issue](https://github.com/AviTewari/Customer-Churn-Prediction-Platform/issues) or submit a PR. 

Happy coding!