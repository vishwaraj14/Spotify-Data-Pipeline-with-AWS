# Spotify-Data-Pipeline-with-AWS

This project extracts, transforms, and loads Spotify playlist data into AWS using a serverless architecture with AWS Lambda, Amazon S3, AWS Glue, and Amazon Athena. It showcases a full ETL pipeline built with Python, Spotipy (Spotify API), and AWS services.

## Architecture Diagram

![Spotify ETL Architecture](ETL.png)

## Overview

- **Source**: Spotify API  
- **Destination**: Amazon S3, AWS Glue Catalog, Amazon Athena  
- **Trigger**: AWS CloudWatch (daily)  
- **Processing**: AWS Lambda (Python functions)  
- **Data Output**: CSVs for Albums, Artists, and Songs  

## ETL

### 1. Extract

- CloudWatch Event Rule triggers the Lambda function daily.  
- Lambda Function (Extraction): `spotify_api_data_extract.py`  
- Authenticates with the Spotify API using Spotipy.  
- Downloads playlist data and stores it as JSON in an S3 bucket under `raw_data/to_processed/`.

### 2. Transform

- Trigger: S3 object creation triggers another Lambda function.  
- Lambda Function (Transformation): `spotify_data_transformation.py`  
- Reads raw JSON files from S3.  
- Extracts and transforms structured albums, artists, and songs data.  
- Stores transformed data as CSV files in:
  - `transformed_data/album_data/`
  - `transformed_data/artist_data/`
  - `transformed_data/songs_data/`  
- Moves processed raw data to `raw_data/processed/`.
