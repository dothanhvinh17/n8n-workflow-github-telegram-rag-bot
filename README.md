# n8n Workflow: GitHub Knowledge Base → Telegram RAG Bot with Qwen

> 🏆 **n8n Verified Creator Workflow**  
> This workflow has been reviewed and approved by the n8n team.  
> 👤 Creator: [Do Thanh Vinh (Kevin Do)](https://github.com/dothanhvinh17)  
> 🔗 Live demo & docs: [vinhautomation.com/en/tools/github-telegram-rag-bot-qwen](https://www.vinhautomation.com/en/tools/github-telegram-rag-bot-qwen/)  
> ⬇️ Download workflow: [n8n.io/workflows/15570](https://n8n.io/workflows/15570-turn-a-github-knowledge-base-into-a-telegram-rag-bot-with-qwen-via-openrouter/)

## 🎯 What It Does

This workflow turns a plain JSON file in a GitHub repository into a fully functional **Telegram chatbot with Retrieval-Augmented Generation (RAG)** — no Pinecone, no Qdrant, no vector database, no extra subscription.

**Perfect for:** Customer support bots, internal FAQ systems, product Q&A, or any knowledge base under a few hundred entries.
[Telegram User] → [n8n Webhook] → [Keyword Matching] → [Qwen via OpenRouter] → [Telegram Reply]
↓
[GitHub JSON Knowledge Base]


## ✨ Key Features

### 🔹 Zero-Cost RAG Without Vector Database
- Retrieval runs entirely locally using **keyword matching** — no embeddings, no vector math, no API calls for retrieval
- Works best with small-to-medium knowledge bases (up to ~500 entries) focused on a specific topic
- Questions are split into words, scored against entries by overlap count, top 2 matches selected as context

### 🔹 Smart Validation & Robust Error Handling
- Strict input validation: `/ask` without question → instant format guidance
- Comprehensive error handling: missing GitHub files, invalid tokens, empty LLM responses → specific user-friendly messages
- Never leaves user hanging — every edge case triggers a clear notification

### 🔹 Easy Customization & Extensibility
- Swap LLMs freely: GPT-4o, Claude, Gemini, or self-hosted — just change model name/base URL
- Add knowledge by editing the JSON file on GitHub — no redeployment needed
- Automatic multi-language support: bot responds in the same language as the user's question

## 🚀 Quick Start

### Prerequisites
- ✅ n8n instance (self-hosted or cloud)
- ✅ Telegram Bot Token (via @BotFather)
- ✅ GitHub Personal Access Token (Fine-grained, read-only, repo-scoped)
- ✅ OpenRouter API Key (or any OpenAI-compatible endpoint)

### Setup Steps
1. **Configure GitHub**: Create Fine-grained PAT → Add GitHub credential in n8n → Configure "get gh file" node with your repo owner/name/path
2. **Prepare Knowledge Base**: Create a JSON file as an array, each entry with a `"text"` field:
   
   ```json
   [
     { "text": "Your FAQ entry here" },
     { "text": "Another knowledge snippet" }
   ]

4. **Connect Telegram & OpenRouter**: Add Telegram Bot credential to all 4 Telegram nodes + OpenRouter credential to the Qwen model node
5. **Activate**: Enable workflow → Send `/ask <your question>` to your Telegram bot to test

## 🔐 Security & Anonymization

This repo is for **educational purposes only**:

- ❌ No production credentials or API keys included
- ❌ No real client data or proprietary business logic
- ❌ Workflow JSON (if added) will have all credentials stripped

> Always store secrets in n8n credentials manager or environment variables — never in code.

## 🧩 Workflow Structure (High-Level)

| Node Group | Purpose |
|------------|---------|
| **Telegram Trigger** | Listen for `/ask <question>` commands |
| **Input Validator** | Check question length/format → early return if invalid |
| **GitHub Fetch** | Pull knowledge base JSON from your repo |
| **Keyword Matcher** | Score question words against entries → select top 2 |
| **Qwen via OpenRouter** | Generate answer using selected context + user question |
| **Error Handler** | Catch & format errors → user-friendly Telegram reply |
| **Response Sender** | Deliver final answer (or error message) back to user |

## 📈 What's Next? (Extending This Workflow)

This workflow is intentionally simple — simple means cheap, stable, easy to debug. When your use case grows, consider:

| Enhancement | When to Add |
|-------------|-------------|
| **Vector Search** | Knowledge base >500 entries, keyword matching not precise enough |
| **Multi-Source KB** | Pull from Notion, Google Sheets, multiple GitHub files |
| **Conversation Memory** | Users need follow-up questions without repeating context |
| **Web Widget** | Serve chat on website via Webhook trigger alongside Telegram |
| **Auto-Sync Index** | Watch GitHub file for changes → rebuild search index automatically |

## 💡 Cost Note

- ✅ Keyword matching: **Free** (runs locally in n8n)
- ⚠️ LLM tokens: **Billed by OpenRouter** per request
- 📊 For knowledge bases of a few hundred entries, cost per request is minimal (~$0.001-0.01 depending on model)

> Monitor usage via OpenRouter dashboard if running at high frequency.

## 🤝 Contributing & Feedback

- Found a bug in the anonymized example? → Open an issue
- Have an improvement idea? → Submit a PR
- Want to discuss a similar use case? → Email [vinh@vinhautomation.com](mailto:vinh@vinhautomation.com)

## 📄 License

MIT License — Free to use, modify, and share for learning purposes.  
Not for commercial resale without prior agreement.

---

🔗 **More by this creator:**  
[github.com/dothanhvinh17](https://github.com/dothanhvinh17) \| [vinhautomation.com/en/tools](https://www.vinhautomation.com/en/tools) \| [n8n.io/creators/dothanhvinh](https://n8n.io/creators/dothanhvinh)
