# 🛠️ Local Setup Guide

Follow these steps to get VenueFlow running on your machine in under 5 minutes.

## 1. Prerequisites
- Node.js (v18+)
- npm (v10+)
- Firebase Project setup

## 2. Clone and Install
```bash
git clone <your-repo-url>
cd venueflow
npm install
```

## 3. Environment Config
1. Create a `.env` file in the root.
2. Copy contents from `.env.example`.
3. Add your `VITE_GOOGLE_MAPS_API_KEY`.
4. Add your Firebase config object.

## 4. Run Development Server
```bash
npm run dev
```
The app will be available at `http://localhost:3000`.

## 5. Running Tests
```bash
# Unit Tests
npm run test

# E2E Tests
npm run test:e2e
```
