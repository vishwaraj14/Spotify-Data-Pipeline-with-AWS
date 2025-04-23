# Spotify-Data-Pipeline-with-AWS
This project extracts, transforms, and loads Spotify playlist data into AWS using a serverless architecture with AWS Lambda, Amazon S3, Glue, andAthena. It showcases a full ETL pipeline built with Python, Spotipy (Spotify API), and AWS services.

## Project Structure
spotify-etl-project/
│
├── lambda/
│   ├── spotify_api_data_extract.py       # Extracts playlist from Spotify API
│   └── spotify_data_transformation.py    # Transforms raw JSON to structured CSV
│
├── architecture/
│   └── architecture-diagram.png          # Visual representation of the AWS pipeline
│
├── README.md                             # You're here!

## 📌 Architecture Diagram

![Spotify ETL Architecture]("Screenshots\ETL.png")


## Overview
-Source: Spotify API
-Destination: Amazon S3, AWS Glue Catalog, Amazon Athena
-Trigger: AWS CloudWatch (daily)
-Processing: AWS Lambda (Python functions)
-Data Output: CSVs for Albums, Artists, and Songs

## ETL
# 1. Extract
-CloudWatch Event Rule ###triggers the Lambda function daily.
-Lambda Function (Extraction): `spotify_api_data_extract.py` 
-Authenticates with the Spotify API using Spotipy.
-Downloads playlist data and stores it as JSON in an S3 bucket under raw_data/to_processed/.

# 2. Transform
-Trigger: S3 object creation triggers another Lambda.
-Lambda (Transformation):
-Reads raw JSON files from S3.
-Extracts structured albums, artists, and songs.

-Stores transformed CSVs in:
 -transformed_data/album_data/
 -transformed_data/artist_data/
 -transformed_data/songs_data/

Moves processed raw data to raw_data/processed/.

# 3. Load
-AWS Glue Crawler scans the transformed CSVs.
-AWS Glue Catalog stores table schemas.
-Amazon Athena enables SQL queries on structured data.

