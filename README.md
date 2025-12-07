# Embedding API Service

This service generates embeddings using the model:
- sentence-transformers/all-MiniLM-L6-v2

Endpoint:
POST /embed

# Embed-Service: Text to Embedding API

This is a simple Python API that converts text into vector embeddings using the **sentence-transformers MiniLM-L6-v2 model**.  
These embeddings can be used for **semantic search**, **recommendations**, or any AI vector similarity tasks.

---

## Features

- Generate **384-dimensional embeddings** for any text
- Simple REST API: `POST /embed`
- Cross-origin support (CORS enabled) — can be called from Android, web, or other clients
- Lightweight and free to deploy

---

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/embed-service.git
cd embed-service
```

### 2. Install dependencies
Make sure you have Python 3.8+ installed. Then run:
```bash
pip install -r requirements.txt
```
### 3. Run the API locally
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```
- The API will be available at: http://localhost:8000/embed
- The --reload flag allows live code updates during development

### Test the API
You can use Postman, curl, or your browser to test:
```bash
curl -X POST http://localhost:8000/embed \
    -H "Content-Type: application/json" \
    -d '{"text": "Hello world"}'
```
Response:

{
  "embedding": [0.0023, -0.034, ..., 0.12]  // 384 numbers
}

### 5. Deploy to Railway (optional)

#### 1. Sign in to Railway

#### 2. Click New Project → Deploy from GitHub

#### 3. Select your embed-service repo

#### 4. Build command:
```bash
pip install -r requirements.txt
```

#### 5. Start command:
```bash
uvicorn main:app --host 0.0.0.0 --port $PORT
```

#### 6. Railway gives you a public URL, e.g.:
https://your-embed-service.up.railway.app/embed

Your Android app can now call this API.

### 6. Using in Android

#### 1. Make a POST request to /embed with JSON body:

{
  "text": "cashier job in Kuala Lumpur"
}


#### 2. The API returns the embedding vector, which you can send to Supabase:

{
  "embedding": [0.0023, -0.034, ..., 0.12]
}


#### 3. Use this embedding with your Supabase RPC:

SELECT *
FROM jobs
ORDER BY embedding <-> '[embedding vector]'
LIMIT 20;

#### 7. Notes & Tips

- Model consistency is important: Always use all-MiniLM-L6-v2 both when creating embeddings and searching.

- Small model = low memory usage: Perfect for free-tier Railway deployment

- CORS is enabled: Your app can call the API from Android or browser

- Sleeping: Free-tier services may sleep after 1 hour of inactivity. First request may be slower.