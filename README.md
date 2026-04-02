# Real-Time-Fare-Prediction-with-Spark-Streaming-ML
This project explores how real-time data streams can be combined with machine learning to generate live predictions. Using Apache Spark’s Structured Streaming and MLlib, the system simulates incoming trip data, processes it on the fly, and produces fare-related insights.
Instead of treating streaming and ML as separate pieces, this project connects them into a single pipeline — from data ingestion to prediction.
⚙️ What This Project Does
At a high level, the system:
Simulates real-time trip data
Processes incoming data streams using Spark
Applies trained machine learning models
Generates predictions instantly
Performs time-based aggregations to analyze trends
🧠 Core Idea
There are two different streaming scenarios implemented:
1. Instant Fare Prediction (Task 4)
This part focuses on predicting fares for each incoming trip in real time.
A Linear Regression model is trained using historical data
The distance_km field is transformed into features using VectorAssembler
The trained model is saved and reused during streaming
As data streams in:
Each record is passed through the model
Predictions are generated immediately
Output per record includes:
trip_id
driver_id
distance_km
fare_amount
predicted_fare
deviation
You’ll see results printed for every micro-batch processed by Spark.
2. Trend Prediction with Windowing (Task 5)
This part shifts from individual predictions to pattern analysis over time.
Streaming data is grouped using sliding time windows
The system calculates average fare per window
A second model predicts the next expected average fare
Unlike Task 4:
Output is not continuous
Results appear only when enough data exists in a window
Output per window includes:
window_start
window_end
avg_fare
predicted_next_avg_fare
🧰 Tech Stack
Python 3
Apache Spark (PySpark)
Spark MLlib
Faker (for simulating streaming data)
🧩 How It’s Organized

Handson_L10/
│
├── task4.py                  # Real-time fare prediction
├── task5.py                  # Window-based aggregation + prediction
├── data_generator.py         # Simulates streaming data
├── training-dataset.csv      # Model training data
│
├── models/
│   ├── fare_model/           # Model used in Task 4
│   └── fare_trend_model_v2/  # Model used in Task 5
│
└── README.md
Running the Project
1. Setup
Bash
python3 -m venv venv
source venv/bin/activate
pip install pyspark numpy faker
2. Run Real-Time Prediction (Task 4)
You’ll need two terminals:
Terminal 1:
Bash
python3 task4.py
 
<img width="975" height="567" alt="image" src="https://github.com/user-attachments/assets/a63982a5-5cfe-4774-bef6-e8ff88e22c17" />

Terminal 2:
Bash
python3 data_generator.py
4. Run Window-Based Prediction (Task 5)
Again, use two terminals:
Terminal 1:
Bash
python3 task5.py
<img width="975" height="181" alt="image" src="https://github.com/user-attachments/assets/deb956f6-229b-4bce-b05e-5120530d4b8d" />

Terminal 2:
Bash
python3 data_generator.py
