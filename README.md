(the page is under development)


# ELK (Elastic search, Logstash, Kibana) for monotoring logs of a Node.js Application


In this demo I am setting up a logs' monitoring solution based on ELK stack for a sample NodeJS app used in a series of previous projects.

The Node.js application is based on two microservices: the frontend interface performing CRUD operations on the backend (MySQL database) and rendering the results.

<details markdown=1><summary markdown="span">Details of the Coffee suppliers sample app</summary>

# Coffee suppliers sample app

## Summary
This is a simple CRUD app built with Express.

## Running locally

### 1. Build the local Db
```sql
create DATABASE COFFEE;
use coffee;
create table suppliers(
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  address VARCHAR(255) NOT NULL,
  city VARCHAR(255) NOT NULL,
  state VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  phone VARCHAR(100) NOT NULL,
  PRIMARY KEY ( id )
);
```

### 2. Install and run the server
```zsh
npm install

# define your db vars at start
APP_DB_HOST=localhost \
APP_DB_USER=root \
APP_DB_PASSWORD="" \
APP_DB_NAME=COFFEE \
npm start
```
If you do not set the env vars when starting the app the values 
from `app/config/config.js` will be used

### 3. The app files' structure:

<img width="718" alt="Screenshot 2023-07-10 at 22 07 30" src="https://github.com/otammato/Jenkins_pipeliline_build_deploy_nodejs_kubernetes/assets/104728608/a637f395-fc50-4a20-a9b8-a9f93498cce7">

</details>

<br>

For logging I've chosen Bunyan, a structured logging module for Node.js, to output log records as JSON. This is particularly useful as it makes log parsing in subsequent stages, like Logstash, more straightforward. With Bunyan's structured logs, it becomes easy to filter, search, and analyze logs.

<br>

Further processing and vizualisation of the emitted logs implemented on the ELK stack (Elastic search, Logstash, Kibana). It is a popular set of tools for searching, analyzing, and visualizing data in real-time. Over the years, the stack has grown to include Beats and is sometimes referred to as the Elastic Stack, but ELK remains a popular term.

<details markdown=1><summary markdown="span">Details of the ELK stack</summary>
The ELK stack, which stands for Elasticsearch, Logstash, and Kibana, is a popular set of tools for searching, analyzing, and visualizing data in real-time. Over the years, the stack has grown to include Beats and is sometimes referred to as the Elastic Stack, but ELK remains a popular term. Here's a detailed description of each component:

### 1. **Elasticsearch**

**Overview**: 
Elasticsearch is a distributed, RESTful search and analytics engine. It's built on top of Lucene and provides a means of storing, searching, and analyzing large volumes of data quickly and in near real-time.

**Key Features**:
- **Distributed**: Automatically splits and distributes data across multiple nodes. Supports clustering, sharding, and replication.
- **Full-Text Search**: Built on top of the Lucene library, it provides powerful full-text search capabilities.
- **RESTful API**: Interact with the data stored in Elasticsearch using RESTful API endpoints, returning data in JSON format.
- **Schema-Free**: JSON documents can be stored without a predefined schema, but you can define custom mappings.
- **Scalability**: Can scale out by adding more nodes to the cluster. Handles large amounts of data efficiently.

### 2. **Logstash**

**Overview**: 
Logstash is a server-side data processing pipeline that ingests, transforms, and then sends data to the specified destination. It can take in data from various sources, process it, and send it to various outputs.

**Key Features**:
- **Inputs**: Supports various input plugins to gather data, including logs, metrics, and other telemetry.
- **Filters**: Data can be transformed and enriched using a variety of filter plugins. Common operations include parsing log entries, adding geographical data from IP addresses, and changing field names.
- **Outputs**: Supports various output plugins to send data to destinations like Elasticsearch, cloud services, or even local files.
- **Extensibility**: Has a rich collection of plugins and can be extended with custom plugins as well.

### 3. **Kibana**

**Overview**: 
Kibana is the visualization layer of the ELK stack. It provides search and data visualization capabilities for data indexed in Elasticsearch.

**Key Features**:
- **Dashboards**: Create, share, and embed interactive data visualizations and dashboards.
- **Data Exploration**: Offers a user-friendly interface to search and view data stored in Elasticsearch.
- **Advanced Analytics**: Supports advanced time series analysis, machine learning features, graph exploration, and more.
- **Management & Monitoring**: Kibana also comes with tools for managing and monitoring the Elasticsearch cluster, as well as advanced features like alerting.
- **Extensibility**: Can be customized with plugins and offers integrations with other Elastic tools.

### **How They Work Together**:

- **Data Collection & Processing**: Logstash collects data from various sources. It then processes, transforms, and enriches the data based on user-defined rules.
  
- **Data Storage**: Once processed, Logstash sends the data to Elasticsearch for storage. Elasticsearch indexes the data, making it quickly searchable.
  
- **Visualization & Analysis**: Kibana interfaces with Elasticsearch to search, view, and visualize the data. Users can create custom dashboards in Kibana to monitor and analyze their data.

Together, the ELK stack provides an end-to-end solution for gathering, processing, storing, and visualizing data, making it a popular choice for log and event data management in particular.
</details>

## Technologies used

- ELK stack (Elastic Search + Logstash + Kibana)
- NodeJS
- MySQL
- Docker
- Docker-compose
- NodeJS, npm
- bunyan (a logging library for Node.js that provides structured and extensible logging capabilities)
- AWS Cloud
- AWS EC2 (Linux Ubuntu 22.04)

<br>

## Prerequisites

To test this solution, you need the following prerequisites:

- Linux workstation with Node.js, npm, Git, and Docker installed (I'm using Ubuntu 22.04)
- A sample Node.JS app


<br>

## Architecture

<img width="1000" alt="Screenshot 2023-08-06 at 22 26 34" src="https://github.com/otammato/ELK2/assets/104728608/df9b12dd-3c35-4259-9e52-aad3b621c89c">

<br><br>

The architecture entails the following:

1. **An AWS EC2 instance**: With installed Docker, Git, Node, npm.

2. **A NodeJS app**: Performs simple CRUD operations on the database(MySQL). Utilizes "bunyan" library for logging.

3. **A Docker-compose file**: Launches containers:
   - Elastic Search
   - Logstash
   - Kibana

<br>



<br>
<br>

## Final result
<img width="1000" alt="Screenshot 2023-08-21 at 22 32 05" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/a7b6560f-a7bd-47a2-8133-1eca1d896830">
<img width="1000" alt="Screenshot 2023-08-21 at 22 31 08" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/3a90234d-7a5f-4533-bd5c-a072047f0528">


<br><br>

## Steps:
## 1. Install Docker-compose
- `sudo apt update`
- `sudo apt  install docker-compose`

## 2. Install nodejs and npm
- `sudo apt install nodejs`
- `sudo apt install npm`

## 3. Launch the Docker-compose file (located in the same directory)  
<details markdown=1><summary markdown="span">docker-compose.yml</summary>
version: '3'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.14.0
    container_name: elasticsearch
    environment:
      - discovery.type=single-node
    ports:
      - "9200:9200"
      - "9300:9300"
  logstash:
    image: docker.elastic.co/logstash/logstash:7.14.0
    container_name: logstash
    volumes:
      - ./nodeapp.conf:/usr/share/logstash/pipeline/nodeapp.conf
    ports:
      - "5000:5000"
      - "9600:9600"
  kibana:
    image: docker.elastic.co/kibana/kibana:7.14.0
    container_name: kibana
    ports:
      - "5601:5601"
    environment:
      ELASTICSEARCH_HOSTS: "http://elasticsearch:9200"

</details>

- `docker-compose up`

## 4. Retrieve the ip address of the dockerized logstash container

- `sudo docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' logstash`

## 5. Update the NodeJS files to utilize the 'bunyan' library for logging

Detailed description of the implemented logging solution based on Bunyan and Logstash:

### **Logging Solution Overview**

I've chosen Bunyan, a structured logging module for Node.js, to output log records as JSON. This is particularly useful as it makes log parsing in subsequent stages, like Logstash, more straightforward. With Bunyan's structured logs, it becomes easy to filter, search, and analyze logs.

### **1. Logger Configuration**

#### **Bunyan Logger Setup**

In `config.js`, we've set up the main logger with multiple streams:

- **File Stream**: This saves logs directly to a file (`logs.log`).
  
- **Standard Output Stream**: This stream is directed to the console, so any log emitted by Bunyan also appears on your console.
  
- **Logstash Stream**: This sends logs to Logstash, which can further process the logs and pass them to Elasticsearch, visualize them on Kibana, or forward to any other destination.

This allows for flexibility in logging. For example, in a production environment, you might want to log critical errors to a separate error file, send general logs to Logstash, and omit console logs.

#### **Child Loggers**

We also created child loggers to differentiate the source of the logs. For instance, in `index.js`, we create a child logger with a source attribute set to "app", indicating these logs come from the app.

### **2. Log Forwarding**

#### **Logstash Configuration (not shown in the provided code)**

After Bunyan sends logs to Logstash, Logstash can be configured with input, filter, and output plugins to determine how logs should be ingested, processed, and forwarded.

- **Input**: This will be set up to receive logs on the specified port from Bunyan.

- **Filter**: Allows you to transform logs, like parsing out specific fields, dropping unneeded information, or enhancing logs with extra data.

- **Output**: This could be set to various destinations, such as Elasticsearch, a file, or another service.

### **3. Log Overrides and Middleware**

#### **Overriding Console Methods**

To ensure that every piece of log data (whether someone uses `console.log` or the Bunyan logger directly) gets captured and structured appropriately, we overrode the default `console.log`, `console.warn`, `console.debug`, and `console.error` methods. This ensures a consistent logging mechanism throughout the app.

#### **Middleware for HTTP Request Logging**

We implemented an Express middleware function, `logRequests`, which logs every incoming HTTP request, capturing the method (GET, POST, etc.) and the URL.

### **4. Structured Logging**

One of the primary benefits of using Bunyan is the ability to produce structured logs. This means logs aren't just simple text strings but structured JSON objects that can contain various fields. This structured data makes it much easier to filter, search, and analyze logs, especially in large systems.

For example, when you see the log:

```json
{"name":"combined-log","hostname":"ip-172-31-84-253","pid":4232,"level":30,"msg":"Server is running on port 3000.","time":"2023-08-22T18:48:53.495Z","v":0}
```

It's not just a string message but contains valuable fields: the name of the logger, hostname, process ID, log level, the actual message, timestamp, and even the Bunyan version.

### **Summary**

This solution provides a robust logging system that captures logs from various parts of the application, structures them, and then routes them to appropriate destinations. It's built to be scalable, easy to analyze, and flexible in terms of where logs can be sent and how they can be processed.

<br><br>

<img width="1000" alt="Screenshot 2023-08-21 at 22 23 27" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/d8bea94a-3de3-4614-a172-0fea507a1994">
<img width="1000" alt="Screenshot 2023-08-21 at 22 24 01" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/efaa83da-1589-4737-9b2c-f5652b5c7e6d">
<img width="1000" alt="Screenshot 2023-08-21 at 22 24 38" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/a750f1bc-6d5c-4203-be1a-ed6bd11c74a8">
<img width="1000" alt="Screenshot 2023-08-21 at 22 25 47" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/681b3406-f5a8-4e0d-bf3d-f7457e33a778">
<img width="1000" alt="Screenshot 2023-08-21 at 22 26 04" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/465dd78a-3c17-4fd4-bcc6-2cb5347375e5">



<img width="1000" alt="Screenshot 2023-08-21 at 22 25 07" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/067dccea-11cd-49f7-b61c-efdc6c588e4c">
<img width="1000" alt="Screenshot 2023-08-21 at 22 25 26" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/95e1e230-56c7-40fa-9417-b45559421d51">
<img width="1000" alt="Screenshot 2023-08-21 at 22 25 37" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/a50b9bac-aba0-4492-ba0b-d677bcd98826">

<img width="1000" alt="Screenshot 2023-08-21 at 22 24 24" src="https://github.com/otammato/ELK_monitoring_NodeJS_logs/assets/104728608/56b8f390-011f-469c-b756-69ee23829557">


