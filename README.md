# Toll-Traffic-Streaming-Data-Pipeline

This project simulates toll plaza traffic data and streams it into a Kafka topic, which is then consumed and stored in a MySQL database. The goal is to analyze road traffic data from various toll plazas to help decongest highways by monitoring traffic patterns in real-time.

![Screenshot 2567-10-03 at 16 39 06](https://github.com/user-attachments/assets/fc9f27ab-4fd6-4be5-9ea7-3a625062ec91)

## Project Overview!
The project consists of two main components:
1. **Traffic Data Simulator**: Generates random vehicle data and streams it to a Kafka topic.
2. **Streaming Data Consumer**: Consumes traffic data from the Kafka topic and stores it in a MySQL database.

### Technologies Used
- **Apache Kafka**: For real-time data streaming.
- **MySQL**: To store traffic data.
- **Python**: For generating and consuming Kafka messages, and interacting with the MySQL database.
- **Kafka-Python**: Python library for Kafka integration.
- **MySQL Connector**: Python library to connect to MySQL.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
  - [Running the Kafka Producer (Traffic Simulator)](#running-the-kafka-producer-traffic-simulator)
  - [Running the Kafka Consumer](#running-the-kafka-consumer)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## Installation

### Prerequisites
- **Kafka**: Make sure Kafka is installed and running. You can download it from the [Kafka 3.8.0]([https://kafka.apache.org/](https://downloads.apache.org/kafka/3.8.0/kafka_2.12-3.8.0.tgz)).
- **MySQL**: Install MySQL and create a database named `tolldata`.
- **Python**: Install Python 3.x and the required packages.

### Step-by-Step Setup

1. Clone the repository:
    ```bash
    git clone https://github.com/your-username/toll-traffic-streaming.git
    cd toll-traffic-streaming
    ```

2. Install the required Python libraries:
    ```bash
    pip install kafka-python mysql-connector-python
    ```

3. Set up Kafka:
   - Start the Kafka server:
     ```bash
     bin/kafka-server-start.sh config/kraft/server.properties
     ```
   - Create a Kafka topic named `toll`:
     ```bash
     bin/kafka-topics.sh --create --topic toll --bootstrap-server localhost:9092
     ```

4. Set up the MySQL database:
   - Create a new database:
     ```sql
     CREATE DATABASE tolldata;
     ```
   - Create a table `livetolldata`:
     ```sql
     USE tolldata;
     CREATE TABLE livetolldata (
         timestamp DATETIME,
         vehicle_id INT,
         vehicle_type CHAR(15),
         toll_plaza_id SMALLINT
     );
     ```

## Usage

### Running the Kafka Producer (Traffic Simulator)

The traffic simulator generates random vehicle data and streams it to the Kafka topic. You can run it by executing the following script:

```bash
python traffic_simulator.py

https://github.com/user-attachments/assets/0a782c45-15d3-47eb-b9c0-e35d484f7d08






