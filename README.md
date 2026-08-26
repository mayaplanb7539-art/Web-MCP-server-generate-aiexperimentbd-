# Web-MCP-server-generate-aiexperimentbd-
├── Dockerfile├── README.md├── package.json├── tsconfig.json└── src├── agent.ts     # Core Gemini 3.5 Agent loop &amp; WebMCP function handler├── index.ts     # Express server &amp; Cloud Run HTTP entrypoints└── types.ts     # TypeScript schemas &amp; task state models

# Set GCP Project
gcloud config set project YOUR_PROJECT_ID

# Build Container via Cloud Build
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/bd-ai-agent

# Deploy to Cloud Run
gcloud run deploy bd-ai-agent \\
  --image gcr.io/YOUR_PROJECT_ID/bd-ai-agent \\
  --platform managed \\
  --region us-central1 \\
  --allow-unauthenticated \\
  --set-env-vars GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
curl -X POST [https://bd-ai-agent-xyz.a.run.app/api/agent/task](https://bd-ai-agent-xyz.a.run.app/api/agent/task) \\
  -H "Content-Type: application/json" \\
  -d '{
    "prompt": "Inspect target WebMCP registration endpoint and execute diagnostic parameters"
  }'

files = {
f"{project_dir}/package.json": package_json,
f"{project_dir}/tsconfig.json": tsconfig_json,
f"{project_dir}/src/types.ts": src_types,
f"{project_dir}/src/agent.ts": src_agent,
f"{project_dir}/src/index.ts": src_index,
f"{project_dir}/Dockerfile": dockerfile_content,
f"{project_dir}/README.md": readme_content,
}
for path, content in files.items():
with open(path, "w", encoding="utf-8") as f:
f.write(content)

---

## Spin-Up & Reproducibility Guide

### Prerequisites
- Node.js (v20+)
- Google Cloud SDK (`gcloud`)
- Gemini API Key with access to Gemini 3.5

### 1. Local Setup

```bash
# Clone repository
git clone [https://github.com/your-username/bd-ai-experiment-agent.git](https://github.com/your-username/bd-ai-experiment-agent.git)
cd bd-ai-experiment-agent

# Install dependencies
npm install

# Configure environment
export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
export GOOGLE_APPLICATION_CREDENTIALS="path/to/firestore-credentials.json"

# Launch development server
npm run dev

npm install
export GEMINI_API_KEY="your-api-key"
npm run dev

gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/bd-ai-agent
gcloud run deploy bd-ai-agent \
  --image gcr.io/YOUR_PROJECT_ID/bd-ai-agent \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --set-env-vars GEMINI_API_KEY="your-api-key"

```text?code_stdout&code_event_index=1
Project built successfully! Files created