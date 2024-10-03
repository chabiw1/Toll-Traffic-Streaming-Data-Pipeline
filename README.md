# Toll-Traffic-Streaming-Data-Pipeline

This project simulates toll plaza traffic data and streams it into a Kafka topic, which is then consumed and stored in a MySQL database. The goal is to analyze road traffic data from various toll plazas to help decongest highways by monitoring traffic patterns in real-time.


https://github.com/user-attachments/assets/39d5e993-2275-42f3-ba04-8e139dd3ec90


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

The Kafka producer script (`toll_traffic_generator.py`) generates random vehicle data and streams it to the Kafka topic. The data includes:

- **Vehicle ID**: A random integer ID between 10,000 and 10,000,000.
- **Vehicle Type**: Randomly chosen from `car`, `truck`, and `van`.
- **Timestamp**: The current time.
- **Plaza ID**: A random toll plaza ID between 4,000 and 4,010.

Run the script using:

```bash
python toll_traffic_generator.py
```
This will simulate real-time traffic and send data to the Kafka topic named `toll`. The script will output the details of each vehicle passing through the toll plaza in the console.

### Running the Kafka Consumer
The Kafka consumer script (steam-data-reader.py) reads messages from the Kafka topic and inserts the data into a MySQL table. The data is read, transformed (timestamp formatted), and then written into the livetolldata table.

Run the consumer using:
```python steam-data-reader.py```

The consumer will continuously listen to the Kafka topic and insert the streamed toll traffic data into the MySQL database.

###Project Structure

.
├── README.md                    # Project documentation
├── toll_traffic_generator.py    # Kafka Producer to generate and stream traffic data
├── steam-data-reader.py         # Kafka Consumer to read and store traffic data in MySQL
