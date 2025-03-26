# Spotify Data Pipeline: End-to-End Data Engineering Project

## Overview
This project builds a **complete data pipeline** using the Spotify API and AWS services. The pipeline extracts, transforms, and loads (ETL) Spotify music data into AWS S3 and sets up an analytics layer using AWS Glue and Athena.

## Key Features
- **Data Extraction**: Fetching playlist data from the Spotify API.
- **Automated Processing**: Using AWS Lambda to transform raw data.
- **Storage & Organization**: Storing structured data in S3.
- **Analytics**: Querying data using AWS Glue and Athena.
- **Automated Scheduling**: Running the pipeline on a schedule.

## Tech Stack
- **Python**
- **Spotify API**
- **AWS Lambda**
- **AWS S3**
- **AWS Glue**
- **AWS Athena**

## Project Architecture
The project follows a structured **Extract, Transform, Load (ETL)** pipeline using AWS services:

1. **Extract Phase:**
   - The pipeline fetches data from the **Spotify API**.
   - **AWS Lambda** (triggered by **Amazon CloudWatch**) automates the extraction.
   - The extracted raw data is stored in an **Amazon S3 bucket**.

2. **Transform Phase:**
   - A second **AWS Lambda function** processes and transforms the data.
   - The transformed data is stored in another **S3 bucket**.
   - A trigger mechanism detects new files and starts the transformation.

3. **Load & Analytics Phase:**
   - AWS **Glue Crawler** infers schema from the transformed data.
   - The **AWS Glue Data Catalog** organizes the metadata.
   - **Amazon Athena** is used to run SQL queries on the processed data for analysis.

![Project Architecture](https://github.com/UmangDas/spotify-end-to-end-pipeline-project/blob/main/Screenshot%202025-03-26%20225307.png)

## Steps to Implement
### 1. **Data Extraction from Spotify API**
- Authenticate using **SpotifyClientCredentials**.
- Fetch playlist data including **albums, artists, and tracks**.
- Store raw JSON files in an S3 bucket (`raw_data/to_processed/`).

### 2. **AWS Lambda for Automation**
- Deploy the extraction script on AWS Lambda.
- Configure an **EventBridge trigger** to run it automatically.

### 3. **Data Transformation**
- Process raw JSON data to extract **album, artist, and song details**.
- Convert to structured **CSV format**.
- Store transformed data in `transformed_data/` on S3.

### 4. **Data Storage in AWS S3**
- Maintain structured folders:
  - `raw_data/to_processed/`
  - `raw_data/processed/`
  - `transformed_data/songs_data/`
  - `transformed_data/album_data/`
  - `transformed_data/artist_data/`

### 5. **Building Analytics with AWS Glue & Athena**
- Set up AWS Glue Crawler to create Athena tables.
- Query data using **SQL in Athena**.

Example Query:
```sql
SELECT * FROM spotify_songs WHERE popularity > 80;
```

## Setup Instructions
### 1. Clone the Repository
```sh
git clone https://github.com/your-username/spotify-data-pipeline.git
cd spotify-data-pipeline
```

### 2. Install Dependencies
```sh
pip install -r requirements.txt
```

### 3. Configure Credentials
Update `config/config.json` with **Spotify API credentials** and **AWS S3 bucket details**.

### 4. Run Extraction Manually
```sh
python src/extract.py
```

### 5. Run Transformation
```sh
python src/transform.py
```

### 6. Run Load Script
```sh
python src/load.py
```

## AWS Lambda Deployment
- Zip `aws_lambda.py` with dependencies.
- Deploy to **AWS Lambda**.
- Configure **EventBridge trigger** for scheduled runs.

---
🚀 **Automate Your Data Workflow with AWS & Spotify!**
