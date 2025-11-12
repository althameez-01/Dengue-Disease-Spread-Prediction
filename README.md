This project is a machine learning–powered Flask web application that predicts the risk level of dengue outbreak for a given location based on environmental and epidemiological factors such as temperature, humidity, hospital count, and reported cases.

The system visualizes predictions on an interactive Folium map, automatically detects the geographical area name using OpenStreetMap’s Nominatim API, and provides confidence scores for each risk level.

⚙️ Key Features

Real-time dengue risk prediction using a trained XGBoost model
Interactive Folium map showing risk level and confidence score
Reverse geocoding via Nominatim API to display area names
Confidence thresholding for uncertainty handling
Web form input with user-friendly interface
Robust error handling & data validation
Expandable architecture — add explainability (SHAP), CSV uploads, or batch predictions easily

Machine Learning Model

Algorithm: XGBoost Classifier and Random Forest


Input features:

Latitude

Longitude

Humidity (%)

Temperature (°C)

Number of Hospitals

Number of Cases

Number of Deaths

Day, Month, Year (derived from date)

Output classes:

low, medium, high, very high (mapped from class IDs)

Confidence Score: Probability of the predicted class (if below threshold → labeled uncertain)

Tech Stack
Category	Technologies
Backend	Flask (Python)
ML Framework	XGBoost, scikit-learn, pandas
Frontend	HTML, CSS, Bootstrap
Mapping	Folium (Leaflet.js)
APIs	OpenStreetMap Nominatim Reverse Geocoding
Model Serialization	joblib
Deployment	Gunicorn / Docker (recommended)

Getting Started
1️⃣ Clone the repository
git clone https://github.com/althameez-01/Dengue-Disease-Spread-Prediction.git
cd dengue-risk-prediction

2️⃣ Create a virtual environment
python -m venv venv
source venv/bin/activate   # on Windows use: venv\Scripts\activate

3️⃣ Install dependencies
pip install -r requirements.txt

4️⃣ Add your trained model

Place your trained_xgb_model.pkl file in the root directory.
(Ensure it matches the training feature schema used in app.py.)

5️⃣ Run the application
python app.py


Visit: http://localhost:5000

🌐 API Workflow
/ — Home route

Displays a web form to input:

Latitude, Longitude

Humidity, Temperature

Number of Hospitals, Cases, Deaths

Date (YYYY-MM-DD)

/predict — Prediction route

Validates inputs and parses the date properly.

Calls the trained XGBoost model for risk prediction.

Maps class probabilities to risk levels.

Fetches the area name using Nominatim reverse geocoding.

Generates a Folium map with a colored marker showing prediction details.

Renders result.html with:

Risk Level

Confidence Score

Area Name

Interactive Map

Input Example
Field	Example
Latitude	6.9271
Longitude	79.8612
Humidity	80
Temperature	30
Number of Hospitals	5
Number of Cases	120
Number of Deaths	3
Date	2025-11-12
Output Example

Predicted Risk Level: High
Confidence Score: 0.87
Area: Colombo, Western Province, Sri Lanka
Map: Red marker displayed at input coordinates with details popup

(Add a screenshot here when uploading to GitHub)

Validation & Error Handling

Ensures latitude ∈ [-90, 90], longitude ∈ [-180, 180]

Validates humidity between 0–100

Rejects negative case/death counts

Parses dates safely (datetime.strptime)

Returns JSON error responses with status codes:

400 → invalid input

500 → internal server error

503 → model not loaded

Security & Compliance

joblib.load only loads trusted model files (never user uploads)

Avoid debug=True in production

Use descriptive User-Agent for Nominatim per usage policy

Input sanitization with range checks

Exception logging without exposing stack traces to users

Future Enhancements

Model explainability (SHAP feature importance per prediction)

Probability calibration (Platt / isotonic scaling)

Batch predictions (CSV upload + downloadable results)

Model monitoring & retraining pipeline

Geocoding cache (LRU/Redis to reduce API calls)

REST API endpoint for programmatic use

CI/CD for deployment

Responsive UI with better visual feedback

Contributing

Contributions are welcome!
If you'd like to:

Report a bug 

Propose an enhancement 

Fix a security or performance issue 

Fork the repo → create a new branch → submit a pull request.

Please follow PEP8 and include concise commit messages.

