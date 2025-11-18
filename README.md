🧠 Sensor Platform – Real-Time Industrial IoT Monitoring

This project integrates Node-RED, Elasticsearch, and Kibana into a unified Industrial IoT data pipeline.
It collects real-time data from IFM IO-Link vibration (VVB001) and ultrasonic (UGT594) sensors through IO-Link master AL1306, decodes hex payloads, and visualizes metrics in Kibana dashboards.

All services run using Docker or Kubernetes for full isolation and scalability.

🚀 Features

🌐 Node-RED – Low-code IoT flow automation

⚙️ Custom decoders for IO-Link 20-byte vibration sensor data & ultrasonic distance data

📦 Elasticsearch – Time-series indexing & fast search

📊 Kibana – Real-time dashboards and analytics

☸️ Kubernetes Ready – Deployable on Docker Desktop, EKS, AKS, GKE

🔄 Complete Pipeline: Sensor → Node-RED → Elasticsearch → Kibana

🧩 Architecture Overview
IO-Link Sensors (VVB001, UGT594)
        ↓
     AL1306 IO-Link Master
        ↓
      Node-RED
        ↓
  Elasticsearch (sensor-data index)
        ↓
        Kibana (Dashboards)

🐳 Docker Deployment
1️⃣ Pull or Build the Docker Image
Pull directly from Docker Hub:
docker pull archit05931/sensor-platform

Build locally:
docker build -t archit05931/sensor-platform:latest .
docker push archit05931/sensor-platform:latest

2️⃣ Start the Full Stack
docker-compose up -d

3️⃣ Access Services
Service	URL	Port
Node-RED	http://localhost:1880
	1880
Elasticsearch	http://localhost:9200
	9200
Kibana	http://localhost:5601
	5601
☸️ Kubernetes Deployment
1️⃣ Apply all manifests

(Use all files inside the K8 folder)

kubectl apply -f K8/

2️⃣ Verify Deployment
kubectl get pods -o wide
kubectl get svc

3️⃣ Port Forward for Local Access
kubectl port-forward service/nodered-service 30080:1880
kubectl port-forward service/elasticsearch-service 30082:9200
kubectl port-forward service/kibana-service 30081:5601

4️⃣ Open Services
Service	URL
Node-RED	http://localhost:30080

Elasticsearch	http://localhost:30082

Kibana	http://localhost:30081

⚠️ Important (Node-RED → Elasticsearch):
In the last HTTP request node, set:

POST http://elasticsearch-service:9200/sensor-data/_doc


You should receive a response containing "_id" confirming successful indexing.

⚙️ Node-RED Flow Summary
✔️ Reads sensor data from IO-Link Master (192.168.1.10)
✔️ Decodes:

🌀 Vibration Sensor (VVB001) – 20-byte IO-Link structured packet

🌊 Ultrasonic Sensor (UGT594) – distance measurement

✔️ Sends JSON to Elasticsearch:
http://localhost:9200/sensor-data/_doc

📊 Kibana Visualization Guide

Open Kibana → http://localhost:30081

Go to Stack Management → Index Patterns

Create index pattern:

sensor-data*


Open Discover to view live sensor entries

Build dashboards for:

Vibration RMS, Peak

Ultrasonic distance

Temperature

Health metrics

☁️ Cloud & Scaling

✔ Fully compatible with:

Docker Hub

AWS EKS

Azure AKS

Google GKE

✔ Supports horizontal scaling:

Node-RED replicas

Elasticsearch data nodes

✔ Future-ready for:

Real-time alerts

IoT edge → cloud pipelines

Dashboard sharing

🧑‍💻 Author

Archit Sharma
IoT Developer | Cloud & Edge Integrator

🔗 GitHub Repo
🔗 Docker Hub Image
