# EcoCart AI

> An e-commerce sustainability application designed to evaluate, track, and encourage eco-friendly practices for both sellers and buyers.

## Problem Statement

E-commerce often struggles with transparency regarding the environmental impact of products. Sellers lack actionable insights to improve their sustainability practices and avoid greenwashing. Meanwhile, consumers find it difficult to make informed, eco-friendly choices due to a lack of reliable environmental data and sustainable delivery options.

## Key Features

- **EcoScore Evaluation**: Calculates sustainability scores and assigns "EcoGrades" to products based on material sourcing, packaging, durability, and locality.
- **Green Zone Audits**: Automated sustainability audits that approve, reject, or flag products for review based on their eco-credentials.
- **Seller Improvement System**: AI-driven insights providing actionable feedback to sellers to improve their product sustainability and reduce greenwashing.
- **Impact Tracking**: Tracks individual user environmental impact over time (carbon emissions saved, plastic reduced, trees planted equivalent).
- **Eco-Friendly Checkout**: Allows users to choose green delivery options (grouped shipping) and eco-packaging at checkout to earn rewards.
- **Reward System**: Incentivizes eco-friendly buyer choices and rewards highly sustainable sellers.

## Technology Stack

### Frontend
- **Framework**: React, Vite
- **Styling**: Tailwind CSS, Framer Motion
- **State Management & Data**: Zustand, React Query, Axios
- **Routing**: React Router DOM
- **Visualization**: Recharts

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **Language**: TypeScript
- **Database**: MongoDB (Mongoose)
- **Security & Validation**: Zod, Helmet, Express Rate Limit, JWT, bcryptjs

### ML Service
- **Framework**: FastAPI (Python)
- **Machine Learning**: scikit-learn, XGBoost, SHAP
- **Data Processing**: Pandas, NumPy
- **Server**: Uvicorn

## System Architecture

This project utilizes a scalable microservices-oriented architecture:

1. **Frontend (Port 5173)**: Handles the user interface for Customers, Sellers, and Admins. Communicates with the Backend API.
2. **Backend (Port 5000)**: The core REST API handling product data, user profiles, reward calculations, and rule-based sustainability audits.
3. **ML Service (Port 8000)**: A dedicated Python microservice to evaluate unstructured product data, detect greenwashing, and predict sustainability metrics.

## How the Application Works

1. **Sellers** upload product data.
2. **Backend** sends product data to the **ML Service**.
3. **ML Service** evaluates the product, calculates an EcoScore, assigns an EcoGrade, and generates explanations (via SHAP) and actionable improvements.
4. **Backend** runs a Green Zone Audit (rule-based) to approve, reject, or flag the product based on the ML results.
5. **Buyers** browse products, seeing clear sustainability metrics and EcoGrades.
6. **Buyers** complete checkout with eco-friendly options, reducing their carbon footprint, which is tracked on their dashboard.

## Project Structure

```
Amazon-Relife/
├── backend/          # Node.js/Express API
│   ├── src/          # Source code (models, routes, controllers)
│   ├── package.json  # Backend dependencies
│   └── tsconfig.json # TypeScript configuration
├── frontend/         # React/Vite web application
│   ├── src/          # React components and pages
│   ├── public/       # Static assets
│   ├── package.json  # Frontend dependencies
│   └── vite.config.js# Vite configuration
└── ml-service/       # Python FastAPI application
    ├── app/          # API endpoints and logic
    ├── training/     # ML model training scripts
    ├── evaluation/   # Model evaluation scripts
    └── requirements.txt # Python dependencies
```

## Prerequisites

- **Node.js** (v18+ recommended)
- **npm** (v9+ recommended)
- **Python** (v3.9+ recommended)
- **MongoDB** (Local instance or MongoDB Atlas cluster)

## Installation and Setup

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd Amazon-Relife
```

### 2. Frontend Setup

```bash
cd frontend
npm install
```

### 3. Backend Setup

```bash
cd backend
npm install
```

### 4. ML Service Setup

```bash
cd ml-service
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Mac/Linux:
# source venv/bin/activate

pip install -r requirements.txt
```

## Environment Variables

Create a `.env` file in the `backend` directory based on the provided `.env.example`:

```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/ecocart
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRES_IN=7d
ML_SERVICE_URL=http://localhost:8000
```

## How to Run Locally

You need to run all three services concurrently. Open three separate terminal windows:

### Terminal 1: Backend

```bash
cd backend
npm run dev
```

### Terminal 2: Frontend

```bash
cd frontend
npm run dev
```

### Terminal 3: ML Service

```bash
cd ml-service
# Ensure virtual environment is activated
uvicorn app.main:app --reload --port 8000
```

## Available Commands

### Frontend (`/frontend`)
- `npm run dev`: Starts the Vite development server.
- `npm run build`: Builds the app for production.
- `npm run lint`: Runs ESLint.
- `npm run preview`: Previews the production build locally.

### Backend (`/backend`)
- `npm run dev`: Starts the development server using `nodemon` and `ts-node`.
- `npm run build`: Compiles TypeScript to JavaScript.
- `npm start`: Runs the compiled production code.

## Application Routes

### Frontend Routes (React / Port 5173)

**Customer / Buyer Routes:**
- `/` - Home Page
- `/products` - Browse Sustainability Products
- `/product/:id` - Individual Product Details
- `/cart` - Shopping Cart
- `/checkout` - Green Checkout Flow
- `/dashboard` - Customer Profile & Impact Dashboard

**Seller Routes:**
- `/seller/dashboard` - Seller Dashboard (Manage Products, View EcoScores, Seller Improvements)

**Admin Routes:**
- `/admin/dashboard` - Platform Admin Dashboard

## Future Improvements

- [Planned] Integration with a third-party carbon offset provider API.
- [Planned] Expanded machine learning capabilities for automated image analysis of product packaging.
- [Planned] Advanced analytics dashboard for sellers.

## License / Credits

Based on the existing repository information.
