# 🪂 AFF Skydiving Assistant

AI-powered assistant for AFF (Accelerated Free Fall) skydiving training with RAG knowledge base, real-time weather data, and safety features.

## 🎯 Features

### 🤖 AI Capabilities
- **Bilingual Support**: Automatically detects and responds in Lithuanian or English
- **RAG Knowledge Base**: Pinecone vector store with AFF training rules and procedures
- **Real-time Weather**: Open-Meteo API integration for jump safety assessment
- **Image Analysis**: GPT-4o Vision for weather condition analysis from photos
- **Human-in-the-Loop**: Critical safety questions require human approval

### 🛠️ Technical Stack
- **Platform**: n8n workflow automation
- **AI Model**: OpenAI GPT-4o-mini
- **Vector DB**: Pinecone (email-agent-database index)
- **Storage**: Google Sheets (conversation logging)
- **API**: Open-Meteo (weather data)
- **Interface**: Webhook + HTML frontend

## 📊 Architecture

**Workflow Flow:**

1. **User Input** (localhost) → Webhook receives request
2. **AI Agent** processes with tools:
   - 🗄️ **Pinecone RAG** - AFF training rules & procedures
   - 🌤️ **Weather API** - Real-time jump conditions
   - 🖼️ **Image Analysis** - Weather photo assessment (optional)
3. **Safety Check**:
   - ✅ Normal question → Direct response
   - ⚠️ Critical question → Human approval required
4. **Response** sent to user
5. **Logging** - All conversations saved to Google Sheets

**Data Flow Diagram:**
┌─────────────┐
│ User        │
│ (localhost) │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ Webhook     │
└──────┬──────┘
       │
       ▼
┌─────────────────────────────┐
│ AI Agent                    │
│ ┌─────────────────────┐     │
│ │ Pinecone RAG        │     │
│ │ Weather API         │     │
│ │ Image Analysis      │     │
│ └─────────────────────┘     │
└──────┬──────────────────────┘
       │
       ▼
┌─────────────┐
│ Critical?   │
└──┬──────┬───┘
   │ Yes  │ No
   ▼      ▼
┌──────--┐   ┌──────────┐
│Human   │   │ Response │
│Approval│   └──────────┘
└──┬──--─┘
   │
   ▼
┌──────────┐
│ Response │
└────┬─────┘
     │
     ▼
┌─────────────┐
│Google Sheets│
│ (logging)   │
└─────────────┘

## 🚀 Setup

### Prerequisites
- n8n instance (cloud or self-hosted)
- OpenAI API key
- Pinecone account
- Google Sheets API access

### Installation

1. **Import Workflow**
   - Download `aff-skydiving-assistant.json`
   - In n8n: **Import from File** → Select JSON

2. **Configure Credentials**
   - OpenAI API (2 connections needed)
   - Pinecone API
   - Google Sheets OAuth2

3. **Update Settings**
   - Google Sheets Document ID: `1XbWV2qpe1Zn8dNzt2_G6_KvlAIysITKkTYzEN47Omcc`
   - Sheet name: `Chat History`
   - Webhook path: `7dddf591-4b3f-49fe-b74d-cf45738667f4`

4. **Activate Workflow**
   - Toggle workflow to **Active**

## 💻 Usage

### API Endpoint

```javascript
POST https://your-n8n-instance.com/webhook/7dddf591-4b3f-49fe-b74d-cf45738667f4

// Request body
{
  "message": "Kokia yra minimali aukštis pirmiems šuoliams?",
  "imageUrl": "https://example.com/sky-photo.jpg" // Optional
}

// Response
{
  "answer": "Minimalus aukštis AFF pirmiems šuoliams yra 3000 metrų..."
}
Frontend Example
<!DOCTYPE html>
<html>
<body>
  <input type="text" id="question" placeholder="Ask about AFF...">
  <button onclick="ask()">Ask</button>
  <div id="response"></div>

  <script>
    async function ask() {
      const question = document.getElementById('question').value;
      const response = await fetch('YOUR_WEBHOOK_URL', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ message: question })
      });
      const data = await response.json();
      document.getElementById('response').innerText = data.answer;
    }
  </script>
</body>
</html>
🔒 Safety Features
Critical Question Detection
Workflow automatically detects safety-critical keywords:
English: emergency, accident, injury, danger, critical
Lithuanian: pavojinga, nelaimė, sužeidimas, kritinė
When detected:
Workflow pauses
Human approval required via webhook
Response sent only after approval
Weather Safety Thresholds
Wind speed >7 m/s: Dangerous for beginners
Automatic assessment based on real-time data
📝 Data Logging
All conversations are logged to Google Sheets with:
Timestamp
Question
Answer
Detected language
🎓 Use Cases
Training Questions: "What is the minimum altitude for first jumps?"
Weather Checks: "Is it safe to jump today?"
Image Analysis: Upload sky photo for weather assessment
Safety Procedures: "What to do in emergency situation?"
📈 Evaluation Criteria Met
✅ LLM: AI Agent with tool orchestration
✅ UI: Webhook + HTML interface
✅ Tools: RAG + Google Sheets + HTTP + Webhooks + Human-in-the-loop 
✅ Prompt Engineering: Specific task + zero-shot 
✅ Other: Clean structure + bilingual 
🤝 Contributing
This is an educational project for AI workflow development course.
📄 License
MIT License - feel free to use for educational purposes.
👤 Author
[Gabriele Danilove] - [gabriele.kalvyte@gmail.com]
🙏 Acknowledgments
n8n community
OpenAI GPT-4o
Pinecone vector database
Open-Meteo API
