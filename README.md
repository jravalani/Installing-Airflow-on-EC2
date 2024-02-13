# Apache Airflow Installation on EC2

Welcome to the installation guide for Apache Airflow on an Amazon EC2 instance. This guide will help you set up Apache Airflow, an open-source platform for orchestrating complex workflows, on your EC2 environment.

## Prerequisites

Before you begin, ensure that you have the following prerequisites:

- An active AWS account with an EC2 instance.
- SSH access to your EC2 instance.

## Important Notice
After the release of **Flask Session 0.6**, I was facing difficulties during the instllation. (Date: 13th Feb, 2024)

```bash
AirflowDatabaseSessionInterface(app=flask_app, db=db, table="session", key_prefix="")
TypeError: __init__() missing 6 required positional arguments: 'sequence', 'schema', 'bind_key', 'use_signer', 'permanent', and 'sid_length'
```
To overcome this error I would recommend people to limit the flask session to less than 0.6

```bash
pip install Flask-Session==0.5
```


## Installation Steps

### Step 1: Connect to your EC2 instance

```bash
ssh -i <your-key.pem> ec2-user@<your-ec2-ip>
```

### Step 2: Update and upgrade your system packages

```bash
sudo yum update -y
sudo yum upgrade -y
```

### Step 3: Install required dependencies

```bash
sudo yum install -y python3 python3-pip
```

### Step 4: Install Apache Airflow

```bash
pip3 install apache-airflow
```

### Step 5: Initialize the Airflow database

```bash
airflow db init
```

### Step 6: Start the Airflow web server and scheduler

```bash
airflow webserver --daemon
airflow scheduler --daemon
```

Visit `http://<your-ec2-ip>:8080` in your web browser to access the Airflow web interface.

## Configuration

- Update your Airflow configuration file located at `$AIRFLOW_HOME/airflow.cfg` to customize settings.

## Usage

1. Create your DAGs (Directed Acyclic Graphs) in the `$AIRFLOW_HOME/dags` directory.
2. Access the Airflow web interface to trigger and monitor your workflows.

For more details on DAG creation and Airflow features, refer to the [official documentation](https://airflow.apache.org/docs/stable/).
