
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
│ User │
│ (localhost) │
└──────┬──────┘
│
▼
┌─────────────┐
│ Webhook │
└──────┬──────┘
│
▼
┌─────────────────────────────┐
│ AI Agent │
│ ┌─────────────────────┐ │
│ │ Pinecone RAG │ │
│ │ Weather API │ │
│ │ Image Analysis │ │
│ └─────────────────────┘ │
└──────┬──────────────────────┘
│
▼
┌─────────────┐
│ Critical? │
└──┬──────┬───┘
│ Yes │ No
▼ ▼
┌──────┐ ┌──────────┐
│Human │ │ Response │
│Approval│ └──────────┘
└──┬───┘
│
▼
┌──────────┐
│ Response │
└────┬─────┘
│
▼
┌─────────────┐
│Google Sheets│
│ (logging) │
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
```
## 🔒 Safety Features

### Critical Question Detection

The workflow automatically detects safety-critical keywords in AI responses.

**Monitored keywords:**
- English: emergency, accident, injury, danger, critical
- Lithuanian: pavojinga, nelaimė, sužeidimas, kritinė

**When critical keywords are detected:**
1. Workflow execution pauses automatically
2. Human approval is required via webhook
3. Response is sent to user only after approval

### Weather Safety Thresholds

- Wind speed greater than 7 m/s is considered dangerous for beginners
- Automatic safety assessment based on real-time weather data
- AI provides recommendations based on current conditions

## 📝 Data Logging

All conversations are automatically logged to Google Sheets with the following information:

- **Timestamp** - When the conversation occurred
- **Question** - User's original question
- **Answer** - AI-generated response
- **Language** - Detected language (Lithuanian or English)

This enables conversation analysis, quality control, and workflow improvement based on real usage patterns.

## 🎓 Use Cases

### Training Questions
Example: "What is the minimum altitude for first jumps?"

The AI retrieves information from the Pinecone knowledge base and provides accurate answers based on AFF training materials.

### Weather Checks
Example: "Is it safe to jump today?"

The AI calls the Weather API to get current conditions and evaluates safety based on wind speed, temperature, and other factors.

### Image Analysis
Example: Upload a sky photo URL

The AI analyzes weather conditions from the image using GPT-4o Vision and combines visual analysis with real-time API data.

### Safety Procedures
Example: "What to do in an emergency situation?"

Critical safety questions trigger the Human-in-the-Loop approval process to ensure accurate, verified information.

## 📈 Evaluation Criteria Met

This project fulfills the following course requirements:

- ✅ **LLM** - AI Agent with tool orchestration (4-5 points)
- ✅ **UI** - Webhook plus HTML interface (2 points)
- ✅ **Tools** - RAG, Google Sheets, HTTP, Webhooks, Human-in-the-loop (8 points)
- ✅ **Prompt Engineering** - Specific task with zero-shot prompting (3 points)
- ✅ **Other** - Clean structure and bilingual support (3-4 points)

**Total Score: approximately 20-22 points out of 24+**

## 🤝 Contributing

This is an educational project developed for an AI workflow development course. Contributions, suggestions, and feedback are welcome.

## 📄 License

MIT License - Free to use for educational purposes.

## 👤 Author

**Gabriele Danilove**

📧 Email: gabriele.kalvyte@gmail.com

🔗 GitHub: [github.com/your-username/aff-skydiving-assistant](https://github.com/your-username/aff-skydiving-assistant)

## 🙏 Acknowledgments

Special thanks to:

- **n8n community** - For the excellent workflow automation platform
- **OpenAI** - For GPT-4o-mini and embedding models
- **Pinecone** - For vector database infrastructure
- **Open-Meteo** - For free weather API access

---

**Built with ❤️ for safer skydiving training**
