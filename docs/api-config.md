# API Configuration

## Required API Keys

### 1. OpenAI API
```env
OPENAI_API_KEY=sk-...your-key-here
OPENAI_MODEL=gpt-4
OPENAI_TEMPERATURE=0.3
OPENAI_MAX_TOKENS=1500
```

**Get your key**: https://platform.openai.com/api-keys

### 2. Google Workspace APIs

#### Gmail API
```env
GMAIL_CLIENT_ID=your-client-id
GMAIL_CLIENT_SECRET=your-client-secret
GMAIL_REFRESH_TOKEN=your-refresh-token
```

#### Google Drive API
```env
GDRIVE_CLIENT_ID=your-client-id
GDRIVE_CLIENT_SECRET=your-client-secret
GDRIVE_FOLDER_ID=your-folder-id
```

#### Google Sheets API
```env
GSHEETS_CLIENT_ID=your-client-id
GSHEETS_CLIENT_SECRET=your-client-secret
GSHEETS_SPREADSHEET_ID=your-sheet-id
```

**Enable APIs**: https://console.cloud.google.com/apis

### 3. n8n Configuration
```env
N8N_HOST=your-n8n-instance.com
N8N_PORT=5678
N8N_PROTOCOL=https
```

## Setup Instructions

### OpenAI Setup
1. Create account at openai.com
2. Navigate to API keys section
3. Create new secret key
4. Copy and save securely
5. Add to n8n credentials

### Google APIs Setup
1. Go to Google Cloud Console
2. Create new project
3. Enable required APIs:
   - Gmail API
   - Google Drive API
   - Google Sheets API
4. Create OAuth 2.0 credentials
5. Configure consent screen
6. Add authorized redirect URIs
7. Download credentials JSON

### n8n Credentials
1. Open n8n instance
2. Go to Credentials
3. Add new credential for each service
4. Paste API keys/OAuth details
5. Test connection
6. Save

## Security Best Practices

- Never commit API keys to Git
- Use environment variables
- Rotate keys regularly
- Limit API key permissions
- Monitor API usage
- Enable 2FA on all accounts

## Rate Limits

### OpenAI
- GPT-4: 10,000 tokens/min
- GPT-3.5: 90,000 tokens/min

### Google APIs
- Gmail: 250 quota units/user/second
- Drive: 1,000 requests/100 seconds
- Sheets: 100 requests/100 seconds/user

## Cost Estimation

### OpenAI Costs
- GPT-4: $0.03/1K tokens (input), $0.06/1K tokens (output)
- GPT-3.5: $0.0015/1K tokens (input), $0.002/1K tokens (output)

**Average per resume**: $0.05 - $0.10

### Google Workspace
- Free tier: 15GB storage
- Paid: $6/user/month (Business Starter)

### n8n
- Cloud: $20/month (Starter)
- Self-hosted: Free (infrastructure costs apply)

## Troubleshooting

### OpenAI Errors
- **401 Unauthorized**: Check API key
- **429 Rate Limit**: Reduce request frequency
- **500 Server Error**: Retry after delay

### Google API Errors
- **403 Forbidden**: Check API enablement
- **401 Unauthorized**: Refresh OAuth token
- **429 Quota Exceeded**: Wait or upgrade plan

---

*Keep your credentials secure!*