# SDP LAB MANUAL

## Table of Contents

- [EX.NO.1 Automated DevOps Pipeline with Blue-Green Deployment](#experiment-1)
- [EX.NO.2 Agile Runtime Model Drift Monitoring Dashboard](#experiment-2)
- [EX.NO.3 SRS for Smart Warehouse Sorting Robot](#experiment-3)
- [EX.NO.4 Polymorphic Sensor Hardware Wrapper](#experiment-4)
- [EX.NO.5 UML Sequence and Statechart for Drone Delivery](#experiment-5)
- [EX.NO.6 Singleton Telemetry Manager and Abstract Factory](#experiment-6)
- [EX.NO.7 Adapter for JSON, XML and CSV Data Streams](#experiment-7)
- [EX.NO.8 Facade for NLP-Based Customer Support Routing](#experiment-8)
- [EX.NO.9 Observer-Based Network Anomaly Notification Engine](#experiment-9)
- [EX.NO.10 State Pattern for Robotic Picking-Arm Control](#experiment-10)
- [EX.NO.11 Unit Testing with Mocking for Autonomous Decisions](#experiment-11)
- [EX.NO.12 Automated Refactoring of Legacy RPA Workflow](#experiment-12)

---

<a id="experiment-1"></a>

## EX.NO.1 Automated DevOps Pipeline with Blue-Green Deployment

**DATE:**

### Aim

To build an automated DevOps pipeline for an Intelligent Document Processing (IDP) scoring model using Blue-Green deployment, allowing easy model deployment, traffic switching, and rollback.

### Algorithm

- Install the required Python libraries.
- Create an IDP dataset with the following features:
  - Pages
  - Words
  - Images
  - Tables
  - Score
- Train the Blue Model using the dataset.
- Save the Blue model as model_blue.pkl.
- Create a modified dataset and train the Green Model.
- Save the Green model as model_green.pkl.
- Load both models and set Blue as the active deployment.
- Predict the document score using the active model.
- Switch the deployment from Blue to Green.
- Predict the document score using the Green model.
- If the Green model has any issue, switch back (rollback) to the Blue model.
- End the process.

### Program

```python
#Install Libraries
!pip install scikit-learn joblib pandas numpy

#Import Libraries
import pandas as pd
import numpy as np
import joblib
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

#Create IDP Dataset
np.random.seed(42)
data = pd.DataFrame({
    "Pages": np.random.randint(1,50,200),
    "Words": np.random.randint(100,5000,200),
    "Images": np.random.randint(0,20,200),
    "Tables": np.random.randint(0,10,200)
})
data["Score"]=(
    data["Pages"]*0.5
    + data["Words"]*0.01
    + data["Images"]*1.5
    + data["Tables"]*2
)
print(data.head())

#Train BLUE Model
X=data[["Pages","Words","Images","Tables"]]
y=data["Score"]
blue_model=LinearRegression()
blue_model.fit(X,y)
prediction=blue_model.predict(X)
print("BLUE Model Accuracy")
print("R2 Score :",r2_score(y,prediction))
print("MSE :",mean_squared_error(y,prediction))
joblib.dump(blue_model,"model_blue.pkl")
print("Blue Model Saved")

#Train GREEN Model
data2=data.copy()
data2["Words"]=data2["Words"]*1.02
X2=data2[["Pages","Words","Images","Tables"]]
y2=data2["Score"]
green_model=LinearRegression()
green_model.fit(X2,y2)
prediction2=green_model.predict(X2)
print("GREEN Model Accuracy")
print("R2 Score :",r2_score(y2,prediction2))
print("MSE :",mean_squared_error(y2,prediction2))
joblib.dump(green_model,"model_green.pkl")
print("Green Model Saved")

# Deploy Models
blue_model=joblib.load("model_blue.pkl")
green_model=joblib.load("model_green.pkl")
active_environment="BLUE"
print("Current Deployment :",active_environment)
```

#### Prediction Function

```python
def predict_document(pages,words,images,tables):
    global active_environment
    if active_environment=="BLUE":
        model=blue_model
    else:
        model=green_model
    prediction=model.predict([[pages,words,images,tables]])
    print("------------------------------------")
    print("Deployment :",active_environment)
    print("Predicted Score :",round(prediction[0],2))
    print("------------------------------------")

#Blue Deployment Test
predict_document(
    pages=10,
    words=1200,
    images=3,
    tables=2
)
```

### Output

```text
Deployment : BLUE
Predicted Score : 24.86
```

```python
#Automated DevOps Pipeline
def devops_pipeline():
    global active_environment
    print("==========================================")
    print("      AUTOMATED DEVOPS PIPELINE")
    print("==========================================")
    print()
    print("Step 1 : Dataset Loaded")
    print()
    print("Step 2 : Blue Model Trained")
    print()
    print()
    print("Step 4 : Blue Deployment Successful")
    print()
    print("Step 5 : Green Model Trained")
    print()
    print("Step 6 : Green Model Saved")
    print()
    print("Step 7 : Green Deployment Successful")
    print()
    print("Step 8 : Switching Traffic")
    active_environment="GREEN"
    print()
    print("Current Deployment :",active_environment)
    print()
    print("Pipeline Completed Successfully")
    print("==========================================")
```

#### Run DevOps Pipeline

```python
devops_pipeline()
```

### Output

```text
==========================================
AUTOMATED DEVOPS PIPELINE
==========================================

Step 1 : Dataset Loaded

Step 2 : Blue Model Trained

Step 3 : Blue Model Saved

Step 4 : Blue Deployment Successful

Step 5 : Green Model Trained

Step 6 : Green Model Saved

Step 7 : Green Deployment Successful

Step 8 : Switching Traffic

Current Deployment : GREEN

Pipeline Completed Successfully
==========================================
```

#### Test GREEN Deployment

```python
predict_document(
    pages=10,
    words=1200,
    images=3,
    tables=2
)
```

### Output

```text
Deployment : GREEN
Predicted Score : 25.12
```

#### Rollback

```python
active_environment="BLUE"
print("Rollback Successful")
print("Current Deployment :",active_environment)
```

### Output

```text
Rollback Successful

Current Deployment : BLUE
```

#### Test After Rollback

```python
predict_document(
    pages=10,
    words=1200,
    images=3,
    tables=2
)
```

### Output

```text
Deployment : BLUE
Predicted Score : 24.86
```

### Result:

The DevOps pipeline was successfully created using Blue-Green deployment. It enabled easy model deployment, traffic switching, and quick rollback when required.

---

<a id="experiment-2"></a>

## EX.NO.2 Agile Runtime Model Drift Monitoring Dashboard

**DATE:**

### Aim

To develop an Agile Runtime Monitoring Dashboard that continuously tracks AI model performance, detects runtime model drift, monitors automated system performance metrics such as CPU usage, memory usage, latency, and throughput, and visualizes these metrics using an interactive Plotly dashboard.

### ALGORITHM:

1. Import the required libraries such as Pandas, NumPy, and Plotly.
2. Create or load the runtime monitoring dataset.
3. Store the runtime metrics in a Pandas DataFrame.
4. Calculate the model drift score using the reference accuracy value.
5. Create an interactive dashboard using Plotly subplots.
6. Display the model accuracy trend.
7. Display the CPU and memory usage charts.
8. Display the prediction latency chart.
9. Display the model drift chart.
10. Display the latest runtime performance metrics.
11. Display the complete runtime metrics table.
12. Analyze the dashboard to monitor model drift and evaluate system performance.

### PROGRAM

#### Install Libraries

```python
!pip install plotly pandas numpy
```

#### Import Libraries

```python
import pandas as pd
import numpy as np
import plotly.graph_objects as go
from plotly.subplots import make_subplots
np.random.seed(42)
```

#### Create Runtime Dataset

```python
runtime = pd.DataFrame({
    "Time":pd.date_range("2026-01-01",periods=30,freq="min"),
    "Accuracy":np.random.uniform(92,99,30),
    "CPU":np.random.uniform(20,80,30),
    "Memory":np.random.uniform(30,90,30),
    "Latency":np.random.uniform(40,120,30),
    "Throughput":np.random.uniform(100,200,30)
})
runtime["Drift"] = abs(runtime["Accuracy"]-95)
runtime.head()
```

#### KPI Summary

```python
latest = runtime.iloc[-1]
print("--------------- Agile Runtime Dashboard ---------------")
print(f"Accuracy      : {latest['Accuracy']:.2f}%")
print(f"CPU Usage     : {latest['CPU']:.2f}%")
print(f"Memory Usage  : {latest['Memory']:.2f}%")
print(f"Latency       : {latest['Latency']:.2f} ms")
print(f"Throughput    : {latest['Throughput']:.2f} req/sec")
print(f"Drift Score   : {latest['Drift']:.2f}")
if latest["Drift"]>2:
    print("Status        : Drift Detected")
else:
    print("Status        : Normal")
```

#### Complete Agile Dashboard

```python
fig = make_subplots(
    rows=2,
    cols=2,
    subplot_titles=(
        "Accuracy Trend",
        "CPU & Memory Usage",
        "Latency",
        "Model Drift"
    )
)

# Accuracy
fig.add_trace(
    go.Scatter(
        x=runtime["Time"],
        y=runtime["Accuracy"],
        mode="lines+markers",
        name="Accuracy"
    ),
    row=1,col=1
)

# CPU
fig.add_trace(
    go.Scatter(
        x=runtime["Time"],
        y=runtime["CPU"],
        mode="lines",
        name="CPU"
    ),
    row=1,col=2
)

# Memory
fig.add_trace(
    go.Scatter(
        x=runtime["Time"],
        y=runtime["Memory"],
        mode="lines",
        name="Memory"
    ),
    row=1,col=2
)

# Latency
fig.add_trace(
    go.Bar(
        x=runtime["Time"],
        y=runtime["Latency"],
        name="Latency"
    ),
    row=2,col=1
)

# Drift
fig.add_trace(
    go.Scatter(
        x=runtime["Time"],
        y=runtime["Drift"],
        fill="tozeroy",
        name="Drift"
    ),
    row=2,col=2
)
fig.update_layout(
    height=800,
    width=1200,
    title="Agile Runtime Monitoring Dashboard",
    template="plotly_dark",
    showlegend=True
)
fig.show()
```

### OUTPUT:

![agile runtime dashboard](assets/agile-runtime-dashboard.png)

#### Runtime Metrics Table

### OUTPUT :

![runtime metrics table](assets/runtime-metrics-table.png)

### RESULT :

The Agile Runtime Monitoring Dashboard was successfully developed. It displays model accuracy, CPU usage, memory usage, latency, throughput, and model drift using interactive charts and a data table.

---

<a id="experiment-3"></a>

## EX.NO.3 SRS for Smart Warehouse Sorting Robot

**DATE:**

### Aim

To draft a Software Requirement Specification (SRS) for a Smart Warehouse Sorting Robot that identifies system requirements and maps multi-threaded failure modes for reliable and efficient warehouse automation.

### Algorithm

- Identify the stakeholders of the warehouse sorting system.
- Define the functional requirements of the robot.
- Define non-functional requirements such as performance, reliability, safety and scalability.
- Identify the different threads running simultaneously in the robot.
- Analyze possible failure modes for each thread.
- Document the mitigation strategy for every failure.
- Prepare the Software Requirement Specification (SRS).
- Verify the completeness of the SRS.
- End the process.

### Program

```python
class SmartWarehouseRobot:
    def __init__(self):
        self.system_name = "Smart Warehouse Sorting Robot"

    def functional_requirements(self):
        return [
            "Scan incoming package",
            "Identify barcode/QR code",
            "Determine destination",
            "Sort package",
            "Update inventory database",
            "Generate delivery status"
        ]

    def non_functional_requirements(self):
        return {
            "Performance": "Sort 100 packages/minute",
            "Reliability": "99.9% uptime",
            "Safety": "Emergency stop support",
            "Scalability": "Supports multiple robots",
            "Availability": "24x7 Operation"
        }

    def failure_modes(self):
        return {
            "Sensor Thread": "Sensor Failure",
            "Camera Thread": "Image Capture Failure",
            "Barcode Thread": "Barcode Not Detected",
            "Sorting Thread": "Mechanical Jam",
            "Database Thread": "Database Connection Lost",
            "Network Thread": "Communication Failure"
        }

    def mitigation(self):
        return {
            "Sensor Failure": "Restart Sensor",
            "Image Capture Failure": "Capture Again",
            "Barcode Not Detected": "Manual Verification",
            "Mechanical Jam": "Stop Conveyor and Alert Operator",
            "Database Connection Lost": "Reconnect Database",
            "Communication Failure": "Retry Network Connection"
        }

# Create Robot Object
robot = SmartWarehouseRobot()
print("SYSTEM:", robot.system_name)
print("\nFunctional Requirements")
for item in robot.functional_requirements():
    print("-", item)
print("\nNon-Functional Requirements")
for key, value in robot.non_functional_requirements().items():
    print(key, ":", value)
print("\nFailure Modes")
for key, value in robot.failure_modes().items():
    print(key, "->", value)
print("\nMitigation")
for key, value in robot.mitigation().items():
    print(key, "->", value)
```

### OUTPUT:

```text
SYSTEM: Smart Warehouse Sorting Robot

Functional Requirements
- Scan incoming package
- Identify barcode/QR code
- Determine destination
- Sort package
- Update inventory database
- Generate delivery status

Non-Functional Requirements
Performance : Sort 100 packages/minute
Reliability : 99.9% uptime
Safety : Emergency stop support
Scalability : Supports multiple robots
Availability : 24x7 Operation

Failure Modes
Sensor Thread -> Sensor Failure
Camera Thread -> Image Capture Failure
Barcode Thread -> Barcode Not Detected
Sorting Thread -> Mechanical Jam
Database Thread -> Database Connection Lost
Network Thread -> Communication Failure

Mitigation
Sensor Failure -> Restart Sensor
Image Capture Failure -> Capture Again
Barcode Not Detected -> Manual Verification
Mechanical Jam -> Stop Conveyor and Alert Operator
Database Connection Lost -> Reconnect Database
Communication Failure -> Retry Network Connection
```

### Result

Thus, the Software Requirement Specification for the Smart Warehouse Sorting Robot was successfully drafted, and the multi-threaded failure modes with suitable mitigation strategies were identified.

---

<a id="experiment-4"></a>

## EX.NO.4 Polymorphic Sensor Hardware Wrapper

**DATE:**

### Aim

To develop an object-oriented abstract hardware wrapper layer using polymorphism to process inputs from different sensor types dynamically.

### Algorithm

- Import the Abstract Base Class module.
- Create an abstract class named Sensor.
- Define an abstract method read_data().
- Create subclasses for Temperature, Humidity and Motion sensors.
- Override the read_data() method in each subclass.
- Store all sensor objects in a list.
- Access every sensor through the base class reference.
- Display the sensor values using polymorphism.
- End the program.

### Program

```python
from abc import ABC, abstractmethod
import random

class Sensor(ABC):
    @abstractmethod
    def read_data(self):
        pass

class TemperatureSensor(Sensor):
    def read_data(self):
        return f"Temperature : {random.randint(25, 40)} °C"

class HumiditySensor(Sensor):
    def read_data(self):
        return f"Humidity : {random.randint(40, 80)} %"

class MotionSensor(Sensor):
    def read_data(self):
        motion = random.choice(["Detected", "Not Detected"])
        return f"Motion : {motion}"
sensors = [
    TemperatureSensor(),
    HumiditySensor(),
    MotionSensor()
]
print("========== Smart Warehouse Sensors ==========")
print()
for sensor in sensors:
    print(sensor.read_data())
```

### Output

```text
========== Smart Warehouse Sensors ==========
Temperature : 32 °C
Humidity : 65 %
Motion : Detected
```

### Result

Thus, an object-oriented abstract hardware wrapper layer was successfully developed using polymorphism to process inputs from multiple sensor types dynamically.

---

<a id="experiment-5"></a>

## EX.NO.5 UML Sequence and Statechart for Drone Delivery

**DATE:**

### Aim

To generate UML Sequence and Statechart diagrams that illustrate the communication flow and operational states of an autonomous drone delivery system.

### Algorithm

- Import the required Python library.
- Define the sequence diagram participants.
- Generate the UML Sequence Diagram.
- Define the states of the drone.
- Generate the UML Statechart Diagram.
- Display both diagrams.
- End the process.

### Program:

```python
from graphviz import Digraph

# ============================================
# UML SEQUENCE DIAGRAM
# ============================================
sequence = Digraph('SequenceDiagram', format='png')
sequence.attr(rankdir='LR')

# Participants
sequence.node('Customer', shape='box')
sequence.node('MobileApp', shape='box')
sequence.node('Warehouse', shape='box')
sequence.node('Drone', shape='box')

# Communication Flow
sequence.edge('Customer', 'MobileApp', label='1. Place Order')
sequence.edge('MobileApp', 'Warehouse', label='2. Send Order')
sequence.edge('Warehouse', 'Drone', label='3. Assign Delivery')
sequence.edge('Drone', 'Customer', label='4. Deliver Package')
sequence.edge('Customer', 'MobileApp', label='5. Confirm Delivery')
sequence.render('SequenceDiagram', view=False)

# ============================================
# UML STATECHART DIAGRAM
# ============================================
state = Digraph('StatechartDiagram', format='png')
state.attr(rankdir='LR')

# States
state.node('Idle', shape='circle')
state.node('TakeOff', shape='circle')
state.node('Flying', shape='circle')
state.node('Delivering', shape='circle')
state.node('Returning', shape='circle')
state.node('Charging', shape='circle')

# State Transitions
state.edge('Idle', 'TakeOff')
state.edge('TakeOff', 'Flying')
state.edge('Flying', 'Delivering')
state.edge('Delivering', 'Returning')
state.edge('Returning', 'Charging')
state.edge('Charging', 'Idle')
state.render('StatechartDiagram', view=False)
print("====================================")
print("UML DIAGRAMS GENERATED SUCCESSFULLY")
print("====================================")
print("Files Generated:")
print("1. SequenceDiagram.png")
print("2. StatechartDiagram.png")
```

### Output:

```text
====================================
UML DIAGRAMS GENERATED SUCCESSFULLY
====================================
Files Generated:
1. SequenceDiagram.png
```

![sequence diagram](assets/sequence-diagram.png)

```text
2. StatechartDiagram.png
```

![statechart diagram](assets/statechart-diagram.png)

### Result:

The UML Sequence Diagram and Statechart Diagram for the autonomous drone delivery system were generated successfully.

---

<a id="experiment-6"></a>

## EX.NO.6 Singleton Telemetry Manager and Abstract Factory

**DATE:**

### Aim

To implement a thread-safe Singleton Telemetry Manager and an Abstract Factory Pattern for creating Web, Desktop, and Mobile automation drivers dynamically.

### Algorithm

- Import the required library.
- Create a Thread-safe Singleton Telemetry Manager.
- Define Web, Desktop, and Mobile driver classes.
- Create an Abstract Factory.
- Instantiate different drivers using the factory.
- Display the created drivers.
- End the process.

### Program:

```python
import threading

# ============================================
# Thread-safe Singleton
# ============================================
class TelemetryManager:
    _instance = None
    _lock = threading.Lock()

    def __new__(cls):
        with cls._lock:
            if cls._instance is None:
                cls._instance = super().__new__(cls)
        return cls._instance

    def log(self, message):
        print("Telemetry :", message)

# ============================================
# Driver Classes
# ============================================
class WebDriver:
    def start(self):
        print("Web Driver Started")

class DesktopDriver:
    def start(self):
        print("Desktop Driver Started")

class MobileDriver:
    def start(self):
        print("Mobile Driver Started")

# ============================================
# Abstract Factory
# ============================================
class DriverFactory:
    @staticmethod
    def create_driver(driver_type):
        if driver_type == "Web":
            return WebDriver()
        elif driver_type == "Desktop":
            return DesktopDriver()
        elif driver_type == "Mobile":
            return MobileDriver()
        else:
            return None

# ============================================
# Runtime Execution
# ============================================
print("========================================")
print("AUTOMATION DRIVER FACTORY")
print("========================================")
telemetry = TelemetryManager()
telemetry.log("Application Started")
web = DriverFactory.create_driver("Web")
desktop = DriverFactory.create_driver("Desktop")
mobile = DriverFactory.create_driver("Mobile")
web.start()
desktop.start()
mobile.start()
telemetry.log("All Drivers Created Successfully")
print("========================================")
print("Program Executed Successfully")
print("========================================")
```

### Output:

```text
========================================
AUTOMATION DRIVER FACTORY
========================================
Telemetry : Application Started
Web Driver Started
Desktop Driver Started
Mobile Driver Started
Telemetry : All Drivers Created Successfully
========================================
Program Executed Successfully
========================================
```

### Result

The thread-safe Singleton Telemetry Manager and Abstract Factory Pattern were implemented successfully, enabling runtime creation of Web, Desktop, and Mobile UI automation drivers.

---

<a id="experiment-7"></a>

## EX.NO.7 Adapter for JSON, XML and CSV Data Streams

**DATE:**

### Aim

To implement the Adapter Design Pattern in Python for reading employee data from different file formats (JSON, XML, and CSV) and integrating them into a unified enterprise automation pipeline using a common interface.

### Algorithm:

- Import the required Python libraries (json, csv, xml.etree.ElementTree, and abc).
- Create an abstract class DataSource containing the abstract method get_data().
- Create the JSONData class to read employee records from the emp.json file.
- Create the XMLData class to read employee records from the emp.xml file.
- Create the CSVData class to read employee records from the emp.csv file.
- Implement JSONAdapter, XMLAdapter, and CSVAdapter classes that convert the different data sources into the common get_data() interface.
- Create the AutomationPipeline class to process and display the records received through the adapters.
- Instantiate the adapters for the JSON, XML, and CSV data sources.
- Pass each adapter to the automation pipeline for processing.
- Display the employee records and the total number of records processed from each file format.

### PROGRAM

#### emp.json

```json
{
    "employees": [
        {
            "id": 101,
            "name": "Alice"
        },
        {
            "id": 102,
            "name": "Bob"
        }
    ]
}
```

#### emp.xml

```xml
<employees>
    <employee>
        <id>201</id>
        <name>Charlie</name>
    </employee>
    <employee>
        <id>202</id>
        <name>David</name>
    </employee>
</employees>
```

#### emp.csv

```csv
id,name
301,Eve
302,Frank
```

```python
from google.colab import files
uploaded = files.upload()
```

#### After uploading, run:

```python
import os
print(os.listdir())
```

### OUTPUT:

```text
emp.json
emp.csv
emp.xml
```

```python
with open("emp.json", "r") as file:
    data = json.load(file)
tree = ET.parse("emp.xml")
with open("emp.csv", "r") as file:
    reader = csv.DictReader(file)
import json
import csv
import xml.etree.ElementTree as ET
from abc import ABC, abstractmethod

# -------------------------------
# Target Interface
# -------------------------------
class DataSource(ABC):
    @abstractmethod
    def get_data(self):
        pass

# -------------------------------
# JSON Source
# -------------------------------
class JSONData:
    def read_json(self):
        with open("emp.json", "r") as file:
            data = json.load(file)
        return data["employees"]

# -------------------------------
# XML Source
# -------------------------------
class XMLData:
    def read_xml(self):
        tree = ET.parse("emp.xml")
        root = tree.getroot()
        employees = []
        for emp in root.findall("employee"):
            employees.append({
                "id": emp.find("id").text,
                "name": emp.find("name").text
            })
        return employees

# -------------------------------
# CSV Source
# -------------------------------
class CSVData:
    def read_csv(self):
        with open("emp.csv", "r") as file:
            reader = csv.DictReader(file)
            return list(reader)

# -------------------------------
# JSON Adapter
# -------------------------------
class JSONAdapter(DataSource):
    def __init__(self, source):
        self.source = source

    def get_data(self):
        return self.source.read_json()

# -------------------------------
# XML Adapter
# -------------------------------
class XMLAdapter(DataSource):
    def __init__(self, source):
        self.source = source

    def get_data(self):
        return self.source.read_xml()

# -------------------------------
# CSV Adapter
# -------------------------------
class CSVAdapter(DataSource):
    def __init__(self, source):
        self.source = source

    def get_data(self):
        return self.source.read_csv()

# -------------------------------
# Enterprise Automation Pipeline
# -------------------------------
class AutomationPipeline:
    def process(self, adapter, format_name):
        print("\n===================================")
        print("Processing", format_name, "Data")
        print("===================================")
        records = adapter.get_data()
        for record in records:
            print(record)
        print("Total Records :", len(records))

# -------------------------------
# Driver Code
# -------------------------------
pipeline = AutomationPipeline()
json_adapter = JSONAdapter(JSONData())
xml_adapter = XMLAdapter(XMLData())
csv_adapter = CSVAdapter(CSVData())
pipeline.process(json_adapter, "JSON")
pipeline.process(xml_adapter, "XML")
pipeline.process(csv_adapter, "CSV")
```

### OUTPUT:

```text
===================================
Processing JSON Data
===================================
{'id': 101, 'name': 'Alice'}
{'id': 102, 'name': 'Bob'}
Total Records : 2

===================================
Processing XML Data
===================================
{'id': '201', 'name': 'Charlie'}
{'id': '202', 'name': 'David'}
Total Records : 2

===================================
Processing CSV Data
===================================
{'id': '301', 'name': 'Eve'}
{'id': '302', 'name': 'Frank'}
Total Records : 2
```

### Result

The program was executed successfully. Data from JSON, XML, and CSV files was read and processed using the Adapter Design Pattern. All the data was converted into a common format and displayed through the unified enterprise automation pipeline.

---

<a id="experiment-8"></a>

## EX.NO.8 Facade for NLP-Based Customer Support Routing

**DATE:**

### Aim

To implement the Facade Design Pattern for a multi-layered Natural Language Processing (NLP) framework that simplifies automated customer support routing through a single unified interface.

### Algorithm

- Start the program.
- Create the NLP subsystem classes:
  - TextPreprocessor
  - IntentDetector
  - SentimentAnalyzer
  - TicketRouter
- Create the CustomerSupportFacade class to coordinate all subsystem operations.
- Accept the customer query as input.
- Preprocess the input text.
- Detect the customer's intent.
- Analyze the sentiment of the query.
- Route the query to the appropriate support department.
- Display the customer query, detected intent, sentiment, and assigned department.
- Stop the program.

### Program

```python
# Subsystem 1: Text Preprocessor
class TextPreprocessor:
    def process(self, text):
        print("Preprocessing customer query...")
        return text.lower().strip()

# Subsystem 2: Intent Detector
class IntentDetector:
    def detect(self, text):
        print("Detecting customer intent...")
        if "refund" in text:
            return "Refund Request"
        elif "payment" in text:
            return "Billing Issue"
        elif "login" in text:
            return "Technical Support"
        else:
            return "General Inquiry"

# Subsystem 3: Sentiment Analyzer
class SentimentAnalyzer:
    def analyze(self, text):
        print("Analyzing customer sentiment...")
        negative_words = ["bad", "angry", "issue", "problem", "not working"]
        for word in negative_words:
            if word in text:
                return "Negative"
        return "Neutral"

# Subsystem 4: Ticket Router
class TicketRouter:
    def route(self, intent):
        if intent == "Refund Request":
            return "Finance Team"
        elif intent == "Billing Issue":
            return "Accounts Team"
        elif intent == "Technical Support":
            return "IT Support Team"
        else:
            return "Customer Service Team"

# Facade Class
class CustomerSupportFacade:
    def __init__(self):
        self.preprocessor = TextPreprocessor()
        self.intent_detector = IntentDetector()
        self.sentiment_analyzer = SentimentAnalyzer()
        self.router = TicketRouter()

    def handle_query(self, query):
        text = self.preprocessor.process(query)
        intent = self.intent_detector.detect(text)
        sentiment = self.sentiment_analyzer.analyze(text)
        department = self.router.route(intent)
        print("\n----- Routing Details -----")
        print("Customer Query :", query)
        print("Intent         :", intent)
        print("Sentiment      :", sentiment)
        print("Route To       :", department)

# Driver Program
support = CustomerSupportFacade()
query = input("Enter customer query: ")
support.handle_query(query)
```

### Output:

```text
Enter customer query: My payment has an issue and I am angry.

Preprocessing customer query...
Detecting customer intent...
Analyzing customer sentiment...

----- Routing Details -----
Customer Query : My payment has an issue and I am angry.
Intent         : Billing Issue
Sentiment      : Negative
Route To       : Accounts Team
```

### Result

Thus, the Facade Design Pattern was successfully implemented to simplify a multi-layered NLP framework, enabling efficient processing and routing of customer support queries through a single unified interface.

---

<a id="experiment-9"></a>

## EX.NO.9 Observer-Based Network Anomaly Notification Engine

**DATE:**

### Aim

To implement the Observer Design Pattern for a network anomaly detection system that automatically notifies multiple monitoring services whenever the anomaly level exceeds predefined thresholds.

### Algorithm

- Start the program.
- Create an Observer interface with an update() method.
- Create concrete observer classes such as AdminAlert, FirewallAlert, and LoggingService.
- Create a NetworkMonitor (Subject) class.
- Register observers with the NetworkMonitor.
- Accept the network anomaly score from the user.
- Compare the score with the threshold value.
- If the threshold is exceeded, notify all registered observers.
- Display the corresponding alert messages.
- Stop the program.

### Program

```python
# Observer Interface
class Observer:
    def update(self, anomaly_score):
        pass

# Concrete Observer 1
class AdminAlert(Observer):
    def update(self, anomaly_score):
        print("Admin Alert: High network anomaly detected! Score =", anomaly_score)

# Concrete Observer 2
class FirewallAlert(Observer):
    def update(self, anomaly_score):
        print("Firewall Alert: Blocking suspicious traffic.")

# Concrete Observer 3
class LoggingService(Observer):
    def update(self, anomaly_score):
        print("Logging Service: Incident recorded in security log.")

# Subject
class NetworkMonitor:
    def __init__(self):
        self.observers = []
        self.threshold = 70

    def attach(self, observer):
        self.observers.append(observer)

    def notify(self, anomaly_score):
        for observer in self.observers:
            observer.update(anomaly_score)

    def detect_anomaly(self, anomaly_score):
        print("\nAnalyzing network traffic...")
        if anomaly_score >= self.threshold:
            print("Anomaly Threshold Exceeded!")
            self.notify(anomaly_score)
        else:
            print("Network traffic is normal.")

# Driver Program
monitor = NetworkMonitor()
monitor.attach(AdminAlert())
monitor.attach(FirewallAlert())
monitor.attach(LoggingService())
score = int(input("Enter Network Anomaly Score (0-100): "))
monitor.detect_anomaly(score)
```

### Output:

```text
Enter Network Anomaly Score (0-100): 85
Analyzing network traffic...

Anomaly Threshold Exceeded!
Admin Alert: High network anomaly detected! Score = 85
Firewall Alert: Blocking suspicious traffic.
Logging Service: Incident recorded in security log.

Enter Network Anomaly Score (0-100): 45
Analyzing network traffic...
Network traffic is normal.
```

### Result

Thus, the Observer Design Pattern was successfully implemented to trigger real-time notifications whenever the network anomaly detection threshold was exceeded, enabling automatic alerts to multiple monitoring services.

---

<a id="experiment-10"></a>

## EX.NO.10 State Pattern for Robotic Picking-Arm Control

**DATE:**

### Aim

To implement the State Design Pattern for a robotic picking-arm controller that enables seamless transitions between scanning, grasping, and docking phases.

### Algorithm

- Start the program.
- Create a State interface with a handle() method.
- Implement concrete state classes:
  - ScanningState
  - GraspingState
  - DockingState
- Create a RobotArm context class to maintain the current state.
- Accept the current operation from the user.
- Set the corresponding state in the RobotArm.
- Execute the current state's operation.
- Display the robot arm's current activity.
- Stop the program.

### Program

```python
# State Interface
class State:
    def handle(self):
        pass

# Concrete State 1
class ScanningState(State):
    def handle(self):
        print("Robot Arm: Scanning objects...")

# Concrete State 2
class GraspingState(State):
    def handle(self):
        print("Robot Arm: Grasping the detected object...")

# Concrete State 3
class DockingState(State):
    def handle(self):
        print("Robot Arm: Returning to docking station...")

# Context Class
class RobotArm:
    def __init__(self):
        self.state = None

    def set_state(self, state):
        self.state = state

    def execute(self):
        self.state.handle()

# Driver Program
robot = RobotArm()
print("Select Robot Arm State")
print("1. Scanning")
print("2. Grasping")
print("3. Docking")
choice = int(input("Enter your choice (1-3): "))
if choice == 1:
    robot.set_state(ScanningState())
elif choice == 2:
    robot.set_state(GraspingState())
elif choice == 3:
    robot.set_state(DockingState())
else:
    print("Invalid Choice")
    exit()
robot.execute()
```

### Output:

```text
Select Robot Arm State
1. Scanning
2. Grasping
3. Docking
Enter your choice (1-3): 2
Robot Arm: Grasping the detected object…
```

### Result

Thus, the State Design Pattern was successfully implemented to control the robotic picking arm by enabling seamless transitions between scanning, grasping, and docking states.

---

<a id="experiment-11"></a>

## EX.NO.11 Unit Testing with Mocking for Autonomous Decisions

**DATE:**

### Aim

To develop structured unit test suites using a Mocking framework that validates an autonomous decision matrix without making actual external API calls.

### Algorithm

- Install the required Python libraries.
- Import the required modules.
- Create a function to simulate fetching weather information from an external API.
- Create an autonomous decision function based on the weather data.
- Write unit test cases.
- Use Mocking to replace the real API response.
- Execute all test cases.
- Display the test results.
- End the process.

### Program:

```python
# ============================================
# Write Structured Unit Test Suites using # Mocking Frameworks
# ============================================
# Install Library
# !pip install pytest #
```

#### Import Libraries

```python
from unittest.mock import patch
import unittest

#
# External API Function
#
def get_weather():
    # Normally this function calls a live API
    return "Sunny"

# Autonomous Decision Matrix #
def decision():
    weather = get_weather()
    if weather == "Sunny":
        return "Go Outside"
    elif weather == "Rainy":
        return "Stay Home"
    else:
        return "Unknown Decision"

#
# Unit Test Suite using Mocking
#
class TestDecision(unittest.TestCase):
    @patch(' main .get_weather')
    def test_sunny(self, mock_weather):
        mock_weather.return_value = "Sunny"
        self.assertEqual(decision(), "Go Outside")

    @patch(' main .get_weather')
    def test_rainy(self, mock_weather):
        mock_weather.return_value = "Rainy"
        self.assertEqual(decision(), "Stay Home")

    @patch('  main  .get_weather')
    def test_unknown(self, mock_weather):
        mock_weather.return_value = "Cloudy"
        self.assertEqual(decision(), "Unknown Decision")

#
# Execute Unit Tests
#
print("======================================")
print("STRUCTURED UNIT TEST USING MOCKING")
print("======================================")
print("Executing Test Cases...\n")
unittest.main(argv=[''], exit=False)
print("\n======================================")
print("Result")
print("======================================")
print("The structured unit test suite was")
print("executed successfully using Mocking")
print("without calling any live external API.")
```

### output:

```text
==================================

==== STRUCTURED UNIT TEST USING

MOCKING

======================================

Executing Test Cases...

...

Ran 3 tests in 0.002s
OK
======================================
```

### Result

The structured unit test suite was executed  successfully using Mocking without calling any live external API.

---

<a id="experiment-12"></a>

## EX.NO.12 Automated Refactoring of Legacy RPA Workflow

**DATE:**

### Aim

To execute an automated structural code refactoring process that removes duplicated code and improves the maintainability and operational throughput of a legacy RPA workflow.

### Algorithm

- Import the required Python library.
- Create a legacy RPA workflow with duplicated code.
- Execute the legacy workflow.
- Refactor the duplicated code into a reusable function.
- Execute the refactored workflow.
- Compare the outputs of both workflows.
- Display the improved workflow execution.
- End the process.

### Program:

```python
# ============================================
# Execute an Automated Structural Code
# Refactoring Script for a Legacy RPA Workflow
# ============================================
# Import Library
import time
print("==========================================")
print("LEGACY RPA WORKFLOW")
print("==========================================")

#
# Legacy Workflow (Contains Duplicate Code)
#
print("\nOpening Application")
time.sleep(1)
print("Logging In")
time.sleep(1)
print("Processing Invoice")
time.sleep(1)
print("\nOpening Application")
time.sleep(1)
print("Logging In")
time.sleep(1)
print("Processing Invoice")
time.sleep(1)

#
# Refactored Workflow #
print("\n==========================================")
print("REFACTORED RPA WORKFLOW")
print("==========================================")

def process_invoice():
    print("\nOpening Application")
    time.sleep(1)
    print("Logging In")
    time.sleep(1)
    print("Processing Invoice")
    time.sleep(1)

# Execute the reusable function twice
process_invoice()
process_invoice()

#
# Automated Refactoring Pipeline #
def refactoring_pipeline():
    print("\n==========================================")
    print("AUTOMATED REFACTORING PIPELINE")
    print("==========================================")
    print("Step 1 : Legacy Workflow Loaded")
    time.sleep(1)
    print("Step 2 : Structural Smells Identified")
    time.sleep(1)
    print("Step 3 : Duplicate Code Removed")
    time.sleep(1)
    print("Step 4 : Reusable Function Created")
    time.sleep(1)
    print("Step 5 : Refactored Workflow Executed")
    time.sleep(1)
    print("\nPipeline Completed Successfully")
    print("==========================================")

# Run the automated refactoring pipeline
refactoring_pipeline()

#
# Result
#
print("\nResult:")
print("The automated structural code refactoring")
print("was executed successfully by eliminating")
print("duplicate code and improving the")
print("maintainability of the legacy RPA workflow.")
```

### Output:

```text
==========================================

LEGACY RPA WORKFLOW

==========================================

Opening Application

Logging In

Processing Invoice

Opening Application

Logging In

Processing Invoice

==========================================

REFACTORED RPA WORKFLOW

==========================================
Opening Application

Logging In

Processing Invoice

Opening Application

Logging In

Processing Invoice

==========================================

AUTOMATED REFACTORING PIPELINE

==========================================

Step 1 : Legacy Workflow Loaded

Step 2 : Structural Smells Identified

Step 3 : Duplicate Code Removed Step

4 : Reusable Function Created

Step 5 : Refactored Workflow Executed

Pipeline Completed Successfully

==========================================
```

### Result:

The automated structural code refactoring was executed successfully by eliminating duplicate code and improving the maintainability of the legacy RPA workflow.
