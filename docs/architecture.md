# Workflow Architecture

## System Overview

```
┌─────────────┐
│   Gmail     │ ← New email with resume attachment
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  n8n Trigger│ ← Detects new email
└──────┬──────┘
       │
       ▼
┌─────────────┐
│Google Drive │ ← Uploads resume file
└──────┬──────┘
       │
       ▼
┌─────────────┐
│Text Extract │ ← Converts PDF/DOCX to text
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  OpenAI API │ ← Analyzes resume content
└──────┬──────┘
       │
       ▼
┌─────────────┐
│Parse Results│ ← Structures AI output
└──────┬──────┘
       │
       ▼
┌─────────────┐
│Google Sheets│ ← Stores analysis results
└──────┬──────┘
       │
       ▼
┌─────────────┐
│Notification │ ← Optional: Slack/Email alert
└─────────────┘
```

## Node Details

### 1. Gmail Trigger Node
- **Type**: Trigger
- **Event**: New email received
- **Filters**: 
  - Has attachment: true
  - Subject contains: "resume" OR "application"
  - From: specific domain (optional)

### 2. Google Drive Upload Node
- **Type**: Action
- **Operation**: Upload file
- **Input**: Email attachment
- **Output**: File ID, File URL
- **Folder**: /Resumes/[Year]/[Month]

### 3. Text Extraction Node
- **Type**: Function/Code
- **Supported Formats**: PDF, DOCX, TXT
- **Libraries**: pdf-parse, mammoth
- **Output**: Plain text content

### 4. OpenAI Analysis Node
- **Type**: API Call
- **Model**: GPT-4 or GPT-3.5-turbo
- **Temperature**: 0.3 (for consistency)
- **Max Tokens**: 1500
- **Input**: Resume text + prompt
- **Output**: Structured JSON

### 5. Data Parser Node
- **Type**: Function
- **Operation**: Parse JSON
- **Validation**: Check required fields
- **Error Handling**: Log failures

### 6. Google Sheets Node
- **Type**: Action
- **Operation**: Append row
- **Sheet**: Resume Analysis
- **Columns**: 
  - Timestamp
  - Candidate Name
  - Email
  - Strengths
  - Weaknesses
  - Role Fit
  - Score
  - File URL

### 7. Notification Node (Optional)
- **Type**: Action
- **Channels**: Slack, Email, Telegram
- **Message**: Summary of analysis
- **Trigger**: On successful completion

## Data Flow

```
Email Attachment → File Upload → Text Extraction → AI Analysis → Data Storage → Notification
```

## Error Handling

1. **File Upload Failure**: Retry 3 times, then log error
2. **Text Extraction Failure**: Skip to manual review
3. **OpenAI API Error**: Queue for retry, notify admin
4. **Sheets Write Error**: Store in backup database

## Performance Metrics

- **Average Processing Time**: 30-45 seconds
- **Success Rate**: 95%+
- **Cost per Analysis**: ~$0.05 (OpenAI API)
- **Concurrent Processing**: Up to 10 resumes

## Security Considerations

- OAuth 2.0 for Google APIs
- API keys stored in environment variables
- Resume files encrypted at rest
- Access logs maintained
- GDPR compliant data handling

## Scalability

- **Current**: 100 resumes/day
- **Max Capacity**: 1000 resumes/day
- **Scaling Options**:
  - Add parallel processing
  - Implement queue system
  - Use batch processing for off-peak hours

---

*Architecture designed for reliability and scalability*