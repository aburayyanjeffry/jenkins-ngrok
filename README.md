# 📡 Jenkins + ngrok GitHub Webhook Setup Guide

This guide explains how to expose a local Jenkins server using ngrok and trigger builds automatically from GitHub webhooks. The Jenkinsfile will create a pipeline that will manage an Nginx on Docker. 

---

## 🧰 Prerequisites

- Jenkins installed locally
- Docker installed (optional for pipeline)
- GitHub account + repository
- ngrok installed
- Jenkins running on http://localhost:8080

---

## 📦 Architecture Overview

GitHub → ngrok public URL → Jenkins (/github-webhook/) → Pipeline runs

---

## 🚀 Step 1 — Install ngrok

Install via Homebrew:

```bash
brew install ngrok/ngrok/ngrok
```

Or download from https://ngrok.com/

---

## 🔑 Step 2 — Authenticate ngrok

Get token from https://dashboard.ngrok.com/

```bash
ngrok config add-authtoken YOUR_TOKEN
```

---

## 🌐 Step 3 — Start Jenkins Tunnel

```bash
ngrok http 8080
```

Forwarding URL example:
https://xxxx.ngrok-free.app -> http://localhost:8080

---

## 🔗 Step 4 — Configure GitHub Webhook

GitHub Repo → Settings → Webhooks → Add webhook

Payload URL:
https://YOUR-NGROK-URL/github-webhook/

Content type:
application/json

Events:
Just the push event

---

## 🧠 Step 5 — Configure Jenkins Job

Job → Configure → Build Triggers

Enable:
✔ GitHub hook trigger for GITScm polling

---

## 🔐 Step 6 — Fix CSRF

Jenkins → Manage Jenkins → Configure Global Security

Enable:
✔ Default Crumb Issuer
✔ Enable proxy compatibility

---

## 🧪 Step 7 — Test Webhook

```bash
git add .
git commit -m "test webhook"
git push
```

Expected:
Started by GitHub push by ...

---

## ⚠️ Notes

- ngrok must stay running
- Free ngrok URL changes on restart
- Update GitHub webhook when URL changes

---

## 🧱 Suggested Folder Structure

```bash
project/
├── Dockerfile
├── Jenkinsfile
├── index.html
├── README.md
└── docs/
```
    └── images/

