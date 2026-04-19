# 🌾 Crop Recommendation System

An intelligent crop recommendation system using Machine Learning that provides personalized crop suggestions based on soil parameters and weather conditions.

🌐 check live : https://crop-frontend-6hx9.onrender.com
---

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#️-tech-stack)
- [Quick Start](#-quick-start)
- [Running the Application](#-running-the-application)
- [Project Structure](#-project-structure)
- [Modes & Features](#-modes--features)
- [API Endpoints](#-api-endpoints)
- [Troubleshooting](#-troubleshooting)
- [Development](#-development)

---

## ✨ Features

- **🌐 Live Mode**: Auto-detect location and fetch real-time weather data
- **✍️ Manual Mode**: Enter all parameters manually
- **🤖 Smart Recommendations**: ML-powered crop suggestions using Random Forest
- **🌡️ Weather Integration**: Real-time data from OpenWeather & NASA POWER APIs
- **🎨 Modern UI**: Beautiful React frontend with smooth animations
- **📱 Responsive Design**: Works on desktop, tablet, and mobile
- **🔄 Dual Mode Support**: Switch between live and manual data entry

---

## 🛠️ Tech Stack

### Backend
- **Flask**: Python web framework for REST API
- **Scikit-learn**: Machine Learning (Random Forest Classifier)
- **Pandas**: Data processing
- **Joblib**: Model serialization

### Frontend
- **React**: Modern UI library
- **Vite**: Fast build tool
- **Tailwind CSS**: Utility-first styling
- **Lucide Icons**: Beautiful icons

### APIs
- **OpenWeather API**: Temperature and humidity data
- **NASA POWER API**: Rainfall data (7-day average)
- **IP Geolocation**: Auto location detection

---

## 🚀 Quick Start

### Prerequisites

Before running the application, ensure you have:
1. **Python 3.7+** installed
2. **Node.js 14+** and **npm** installed
3. All required dependencies

### First Time Setup

#### Step 1: Install Backend Dependencies

```bash
# Navigate to backend folder
cd backend

# Install Python dependencies
pip install -r requirements.txt

# If using virtual environment (recommended)
source .venv/bin/activate
pip install -r requirements.txt
```

#### Step 2: Install Frontend Dependencies

```bash
# Navigate to frontend folder (from project root)
cd frontend
npm install
```

---

## 🎯 Running the Application

You have **3 options** to run the application:

### ✅ Option 1: Using Start Script (RECOMMENDED)

```bash
cd backend
chmod +x start_app.sh
./start_app.sh
```

This automatically starts both backend and frontend servers.

### ✅ Option 2: With Virtual Environment

```bash
cd backend
chmod +x activate_and_run.sh
./activate_and_run.sh
```

This activates the virtual environment and starts both servers.

### ✅ Option 3: Manual Start (Two Terminals)

**Terminal 1 - Backend:**
```bash
cd backend
python3 app/main.py
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```

### 🌐 Access the Application

Once servers are running:
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:5001

### 🛑 Stop the Application

Press `Ctrl+C` in the terminal(s) where servers are running.

---

## 📦 Project Structure

```
crop_reccomendation/
├── backend/
│   ├── api/
│   │   ├── weather_api.py      # Weather API integrations
│   │   └── test_weather.py     # API tests
│   ├── app/
│   │   ├── main.py             # Flask server
│   │   ├── utils.py            # Core recommendation logic
│   │   ├── example_modes.py    # Mode examples
│   │   └── test.py             # CLI testing
│   ├── data/
│   │   └── Crop_recommendation.csv
│   ├── model/
│   │   ├── crop_recommendation_model.pkl  # Trained model
│   │   └── scaler.pkl                     # Feature scaler
│   ├── notebooks/              # Jupyter notebooks for training
│   ├── .venv/                  # Virtual environment
│   ├── requirements.txt        # Python dependencies
│   ├── start_app.sh           # Startup script
│   └── activate_and_run.sh    # Startup with venv
├── frontend/
│   ├── src/
│   │   ├── App.jsx            # Main React component
│   │   ├── main.jsx           # Entry point
│   │   └── index.css          # Styles
│   ├── public/                # Static assets
│   ├── package.json           # Node dependencies
│   └── vite.config.js         # Vite configuration
└── README.md                  # This file
```

---

## 🎮 Modes & Features

The system supports **2 primary modes**:

### 🌐 LIVE MODE

**Description**: Fetches real-time weather data from APIs while accepting soil data from manual input.

**Data Sources**:
- **Weather** (from APIs):
  - Temperature: OpenWeather API
  - Humidity: OpenWeather API
  - Rainfall: NASA POWER API (7-day average)
- **Soil** (manual input):
  - Nitrogen (N)
  - Phosphorus (P)
  - Potassium (K)
  - pH value

**When to Use**:
- ✅ Real-time crop recommendations
- ✅ Field applications with GPS
- ✅ Mobile apps with location services
- ✅ When internet connection is available

### ✍️ MANUAL MODE

**Description**: All parameters (weather + soil) are entered manually by the user.

**Data Sources**:
- **All manual input**:
  - Soil: N, P, K, pH
  - Weather: Temperature, Humidity, Rainfall

**When to Use**:
- ✅ Testing with known data
- ✅ Historical data analysis
- ✅ Offline applications
- ✅ Educational/demo purposes
- ✅ No internet connection

### 📊 Comparison

| Feature | LIVE MODE | MANUAL MODE |
|---------|-----------|-------------|
| **Weather Data** | From APIs ✅ | User enters ✍️ |
| **Soil Data** | User enters ✍️ | User enters ✍️ |
| **Internet Required** | Yes | No |
| **Real-time** | Yes | No |
| **Use Case** | Field apps | Testing/Offline |

---

## 🌐 API Endpoints

Once the backend is running, these endpoints are available:

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/health` | Health check |
| GET | `/api/location` | Detect current location |
| POST | `/api/recommend/live` | Get crop recommendation (live mode) |
| POST | `/api/recommend/manual` | Get crop recommendation (manual mode) |

### Example Request (Live Mode)

```bash
curl -X POST http://localhost:5001/api/recommend/live \
  -H "Content-Type: application/json" \
  -d '{
    "N": 90,
    "P": 42,
    "K": 43,
    "ph": 6.5,
    "lat": 30.9,
    "lon": 75.8
  }'
```

### Example Request (Manual Mode)

```bash
curl -X POST http://localhost:5001/api/recommend/manual \
  -H "Content-Type: application/json" \
  -d '{
    "N": 90,
    "P": 42,
    "K": 43,
    "temperature": 25.0,
    "humidity": 70.0,
    "ph": 6.5,
    "rainfall": 150.0
  }'
```

---

## 🐛 Troubleshooting

### Port Already in Use

If you get a "port already in use" error:

**Backend (port 5001):**
```bash
lsof -ti:5001 | xargs kill -9
```

**Frontend (port 5173):**
```bash
lsof -ti:5173 | xargs kill -9
```

### Module Not Found

If you get module import errors:
```bash
cd backend
pip install -r requirements.txt
```

### npm Command Not Found

Install Node.js from: https://nodejs.org/

### Model Not Loading

Ensure these files exist:
- `backend/model/crop_recommendation_model.pkl`
- `backend/model/scaler.pkl`

If missing, retrain the model using the Jupyter notebook in `backend/notebooks/`.

### About the Location Error

**If you see "location error" when starting the server:**

This is **NORMAL** and **NOT a critical error**. Here's why:

1. The app tries to auto-detect your location using free IP geolocation APIs
2. These APIs have rate limits (especially if you restart frequently)
3. If detection fails, it automatically uses a **default location** (Ludhiana, India)
4. The app continues to work perfectly with the default location

**How to handle it:**
- Location is only needed for the "Live Mode" feature
- You can use "Manual Mode" and enter weather data yourself
- Or manually provide latitude/longitude instead of auto-detection

---

## 💻 Development

### Backend Development

The backend uses Flask and provides a REST API. Main files:

- **`backend/app/main.py`**: Flask server and API endpoints
- **`backend/app/utils.py`**: Core ML logic and recommendation functions
- **`backend/api/weather_api.py`**: Weather API integration

### Frontend Development

The frontend uses React with Vite for fast development:

```bash
cd frontend
npm run dev     # Start development server
npm run build   # Build for production
npm run preview # Preview production build
```

### Training the Model

To retrain the machine learning model:

1. Open the Jupyter notebook in `backend/notebooks/`
2. Run all cells to:
   - Load and analyze the dataset
   - Train a new Random Forest model
   - View performance metrics and visualizations
   - Save the updated model files

The notebook includes:
- 📊 Exploratory data analysis
- 📈 Feature importance visualization
- 🎯 Accuracy metrics and classification reports
- 🧪 Sample predictions for verification

### Testing

**Test Backend CLI:**
```bash
cd backend
python3 app/utils.py
```

**Test Weather API:**
```bash
cd backend
python3 api/test_weather.py
```

**Test All Modes:**
```bash
cd backend
python3 app/example_modes.py
```

---

## 📊 Input Parameters

### Soil Parameters
- **Nitrogen (N)**: Nitrogen content in soil (0-140)
- **Phosphorus (P)**: Phosphorus content in soil (0-145)
- **Potassium (K)**: Potassium content in soil (0-205)
- **pH**: Soil pH value (3.5-10)

### Weather Parameters
- **Temperature**: Temperature in Celsius (8-45°C)
- **Humidity**: Humidity percentage (14-100%)
- **Rainfall**: Rainfall in mm (20-300mm)

---

## 🌾 Supported Crops

The model can recommend the following crops:
- Rice
- Maize
- Chickpea
- Kidney Beans
- Pigeon Peas
- Moth Beans
- Mung Bean
- Black Gram
- Lentil
- Pomegranate
- Banana
- Mango
- Grapes
- Watermelon
- Muskmelon
- Apple
- Orange
- Papaya
- Coconut
- Cotton
- Jute
- Coffee

---

## 🔑 API Keys

The application uses the following APIs:

### OpenWeather API
- **Purpose**: Temperature and humidity data
- **Default key included**: For testing purposes
- **Get your own**: https://openweathermap.org/api
- **Location**: Can be changed in `backend/app/main.py`

### NASA POWER API
- **Purpose**: Rainfall data
- **API Key**: Not required (public API)

---

## 📝 Notes

1. Make sure you're in the correct directory before running commands
2. The backend must be running before the frontend can make API calls
3. Default API key is included for OpenWeatherMap (for testing)
4. Location detection uses free APIs and may be rate-limited
5. The app works perfectly even if location detection fails (uses fallback)
6. All shell scripts should be run from the `backend/` folder

---

## 🤝 Contributing

Feel free to contribute to this project by:
1. Forking the repository
2. Creating a feature branch
3. Making your changes
4. Submitting a pull request

---

## 📄 License

MIT License

---

## 🎯 Quick Reference

**Full Stack (Backend + Frontend):**
```bash
cd backend && ./start_app.sh
```

**Backend Only:**
```bash
cd backend && python3 app/main.py
```

**Frontend Only:**
```bash
cd frontend && npm run dev
```

**CLI Test Mode:**
```bash
cd backend && python3 app/utils.py
```

---
