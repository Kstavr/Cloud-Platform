IoT Monitoring System
Overview
This project is an IoT monitoring system using Node-RED, ThingSpeak, RabbitMQ, MinIO, and Keycloak, deployed via Kubernetes. The system gathers sensor data from an ESP32 device, processes it through Node-RED, stores data in MinIO, and manages authentication with Keycloak.

Technologies Used
ESP32 (IoT device for collecting temperature & humidity data)
ThingSpeak (Cloud-based IoT data visualization)
Node-RED (Flow-based programming for IoT data processing)
RabbitMQ (Message broker for distributed communication)
MinIO (Object storage service for storing sensor data)
Keycloak (Identity & Access Management)
Kubernetes (Container orchestration for deployment)
System Architecture
The IoT device (ESP32) sends temperature & humidity data to ThingSpeak via HTTP.

Node-RED fetches the data, processes it, and sends alerts when necessary.
RabbitMQ ensures reliable message passing between components.
MinIO is used for storing historical data.
Keycloak manages user authentication and access control.
Kubernetes handles deployment and scaling.
Setup Instructions
1. Clone the Repository
sh
Αντιγραφή
Επεξεργασία
git clone https://github.com/Kstavr/Cloud-Platform.git
cd Cloud-Platform
2. Deploy Services on Kubernetes
sh
Αντιγραφή
Επεξεργασία
microk8s kubectl apply -f kubernetes/
3. Access the Services
Node-RED: http://<server-ip>:31880
ThingSpeak: https://thingspeak.com/
RabbitMQ Management UI: http://<server-ip>:31672
MinIO UI: http://<server-ip>:32001
Keycloak Admin Console: http://<server-ip>:30080/admin/
4. Configurations
ESP32 Configuration (Arduino)
Modify the ESP32 code with your Wi-Fi credentials and ThingSpeak API Key:

cpp
Αντιγραφή
Επεξεργασία
const char* ssid = "Your_WiFi_Name";
const char* password = "Your_WiFi_Password";
const char* server = "http://api.thingspeak.com/update";
const char* apiKey = "Your_ThingSpeak_API_Key";
Upload the code using Arduino IDE.

RabbitMQ Connection (Node-RED)
Configure AMQP-in and AMQP-out nodes with RabbitMQ credentials.
Use the routing key iot/sensors to send messages.
MinIO Configuration
Create an S3 bucket to store sensor logs.
Update Node-RED function nodes to store JSON data in MinIO.
Keycloak Authentication
Create a new realm (iot-realm) in Keycloak.
Add a client (node-red) for authentication.
Set up users with roles for accessing dashboards.
Usage
Sending Data from ESP32
Once the ESP32 is running, it will:

Read temperature & humidity from the DHT11 sensor.
Send telemetry data to ThingSpeak every 15 seconds.
Viewing Data in Node-RED
Open Node-RED UI (http://<server-ip>:31880).
Check debug messages for received data.
View dashboard graphs for real-time monitoring.
RabbitMQ Messaging
Sensor data is published to RabbitMQ.
Consumers (Node-RED) process the messages.
MinIO Data Storage
Processed data is stored in MinIO.
Can be accessed via S3 API or MinIO dashboard.
Authentication with Keycloak
Access Node-RED and MinIO via Keycloak login.
Admin users can manage devices and settings.
Troubleshooting
ESP32 Not Connecting?
Check Wi-Fi credentials.
Verify ThingSpeak API Key.
No Data in Node-RED?
Ensure ThingSpeak API is correctly configured.
Debug messages in Node-RED console.
RabbitMQ Errors?
Restart RabbitMQ service in Kubernetes.
MinIO Access Issues?
Verify bucket permissions and credentials.
Keycloak Authentication Failing?
Check client ID & secret in the Keycloak admin panel.
Contributors
Kstavr (Project Setup, Kubernetes Deployment, Node-RED Integration)
License
This project is open-source under the MIT License.
