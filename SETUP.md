# Setup Guide

## Prerequisites

- n8n account (cloud or self-hosted)
- Google Workspace account
- OpenAI API key
- Gmail with API access enabled

## Step 1: Setup n8n

1. Create n8n account at n8n.io
2. Create new workflow
3. Name it AI Resume Analyzer

## Step 2: Configure Gmail Trigger

1. Add Gmail Trigger node
2. Set trigger: On new email with attachment
3. Filter: Subject contains Resume or Application
4. Authenticate with Google

## Step 3: Setup Google Drive

1. Add Google Drive node
2. Action: Upload file
3. Map attachment from Gmail
4. Set folder: Resumes

## Step 4: Configure OpenAI

1. Add OpenAI node
2. Model: gpt-4 or gpt-3.5-turbo
3. Add system prompt for analysis
4. Map resume text as input

## Step 5: Setup Google Sheets

1. Add Google Sheets node
2. Action: Append row
3. Map AI output to columns
4. Authenticate with Google

## Step 6: Test Workflow

1. Send test email with resume
2. Check workflow execution
3. Verify data in Google Sheets

## Done!

Your AI Resume Analyzer is now live!