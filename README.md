# 🧠 Intelligent Meeting Summarizer

A transformer-based summarization system that generates concise and accurate summaries of meeting transcripts. Supports both general and query-focused summaries using fine-tuned models (BART and T5). Includes a FastAPI backend and is fully Dockerized for deployment.

---

## 🧩 Problem Statement

In today’s remote/hybrid work environments, meetings are frequent and dense with information. Manually summarizing them is inefficient and error-prone.

**Goal:** Automatically generate relevant, coherent summaries from long meeting transcripts using state-of-the-art NLP models.

---

## 💡 Key Features

- Preprocessing and chunking of the QMSUM dataset
- Fine-tuning of BART-base, T5-base, BART-large-XSum, and BART-large-CNN
- Evaluation with ROUGE, BERTScore, METEOR, BLEU
- FastAPI endpoints for inference (single, batch, and file upload)
- Web UI for transcript upload and visualization
- Fully Dockerized for deployment

---

## 📁 Project Structure

Intelligent_Meeting_Summarizer/
├── app/
│ ├── model/ # Saved fine-tuned models
│ ├── bart_large.py # BART-large-XSum summarization logic
│ ├── bart_large_cnn.py # BART-large-CNN summarization logic
│ ├── main.py # FastAPI routes and app setup
│ ├── schemas.py # Request/response models
├── static/ # CSS, JS assets
├── templates/
│ └── index.html # Upload UI
├── output/ # Generated summaries (optional)
├── requirements.txt # Python dependencies
├── Dockerfile # Docker config


---

## 🚀 Models Trained

| Model             | Description                                      | Best Use Case              |
|------------------|--------------------------------------------------|----------------------------|
| BART-base         | Baseline model, low resource usage              | Small-scale experiments    |
| T5-base           | Text-to-text versatile model                    | Needs tuning               |
| BART-large-XSum   | Abstractive, one-liner summaries                | Concise highlights         |
| BART-large-CNN ✅ | Extractive-abstractive, multi-sentence support | Real-world deployment ✅    |

---

## 📊 Evaluation Summary (BART-large-CNN)

| Metric     | Score   |
|------------|---------|
| ROUGE-1    | 33.52   |
| ROUGE-2    | 9.84    |
| ROUGE-L    | 21.17   |
| ROUGE-Lsum | 29.68   |
| METEOR     | 23.90   |
| BERTScore  | 88.23   |
| BLEU       | 6.10    |

---

## 🏗️ Run Locally (FastAPI)

```bash
# Install dependencies
pip install -r requirements.txt

# Start the API
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000


Visit: http://localhost:8000/ui to access the web interface.

🐳 Run with Docker

docker build -t fnaticdocker106/imesum .

docker run -d -p 8000:8000 fnaticdocker106/imesum
Visit: http://localhost:8000/ui

Push to Docker Hub

docker login
docker push fnaticdocker106/imesum

📡 API Endpoints
🔹 BART-Large (XSum)

POST /bart_large – Single transcript summarization

POST /bart_large/batch – Batch summarization

POST /bart_large/batch_upload_json – Upload JSONL file

🔹 BART-Large-CNN ✅
POST /bart_large_cnn – Single transcript summarization

POST /bart_large_cnn/batch – Batch summarization

POST /bart_large_cnn/batch_upload_json – Upload JSONL file

🔐 Sample cURL
curl -X POST http://localhost:8000/bart_large_cnn \
  -H "Content-Type: application/json" \
  -d '[{"speaker": "Alice", "text": "We discussed the quarterly goals..."}]'


☁️ AWS Deployment Options
Amazon ECS + Fargate: Run as a containerized service with auto-scaling.

AWS App Runner: Directly deploy from Docker Hub with built-in HTTPS, scaling, and load balancing.
