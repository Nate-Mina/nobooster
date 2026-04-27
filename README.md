# Clepto Trap AI Security

Behavioral detection system using AI to identify shoplifting and suspicious activity in real-time.

## Features
- Real-time video analysis using Gemini AI.
- Behavioral detection for shoplifting and falls.
- Automated security logs recorded to Firebase.
- Security Digest summaries.

## Deployment to GitHub Pages

This project is configured to automatically deploy to GitHub Pages via GitHub Actions.

### Steps to enable:
1. Push this code to your GitHub repository.
2. Go to **Settings > Secrets and variables > Actions** in your GitHub repo.
3. Add a **New repository secret**:
   - Name: `GEMINI_API_KEY`
   - Value: Your Google Gemini API Key.
4. The deployment will trigger automatically on pushes to the `main` branch.
5. Once the workflow finishes, go to **Settings > Pages** and set the source to the `gh-pages` branch.

## Local Development
Run `npm install` and then `npm run dev` to start the development server.
