# Project01: NYC Parking Violation 
## Xiang Lin

## Overview

The NYC Open Data project makes freely available data published by NYC agencies and other partners. These datasets range from a few thousand rows to millions, depending on department and time frame.

For this project we will be leveraging a python client of the Socrata API to connect to the Open Parking and Camera Violation API, load the data into Elasticsearch (OpenSearch) instance, and visualize with Kibana (OpenSearch Dashboard).

## Project Breakdown

project01/ \
+-- Dockerfile \
+-- requirements.txt \
+-- src/ \
+-- +-- main.py \
+-- assets/ \
+-- +-- dashboard01.png \
+-- +-- dashboard02.png \
+-- +-- dashboard03.png \
+-- +-- dashboard04.png \
+-- +-- dashboardFull.png \
+-- README

## Techology Used
<pre><code> 
- Software Platform: Docker
- Services: AWS EC2, ElasticSearch (OpenSearch), Kibana (OpenSearch Dashboard)
- Python Libarires: sodapy, requests, argparse, sys, os, json 
</code></pre>


## API Used

[Open Parking and Camera Violations](https://dev.socrata.com/foundry/data.cityofnewyork.us/nc67-uf89)

## Loading into ElasticSearch

Step 1: Build docker image

<pre><code> 
docker build -t bigdataproject1:1.0 .
</code></pre>

Step 2: Run docker container

<pre><code>
docker run \
-e DATASET_ID="nc67-uf89" \
-e APP_TOKEN=" " \
-e ES_HOST=" " \
-e ES_USERNAME=" " \
-e ES_PASSWORD=" " \
-e INDEX_NAME="parkingnyc1.1" \
bigdataproject1:1.0 --page_size=150000
</code></pre>

Step 3: Interchangable Page Size

<pre><code>
bigdataproject1:1.0 --page_size= " page size "
</code></pre>

## Visualized through Kibana 

1. Most Popular Ticket Issuing Agency
    - Traffic
    - Department of Transportation
    - Police Department
    - ...
    
2. Top 10 Violation Type
    - No Parking - Street Cleaning
    - Inspection Sticker - Expired/Missing
    - Photo School Speed Violation
    - Fail to Display Meter Receipt
    - No Standing Zone - Day/Time Limits
    - ...
    
3. Top 10 Total Fines Collected by Violations
    - Inspection Sticker - Expired/Missing: \$1,299,000
    - Photo School Speed Violation: \$1,029,129
    - No Parking - Street Cleaning: \$1,024,990
    - No Standing Zone - Day/Time Limits: \$967,051
    - Fire Hydrant: \$597,011
    - ...
    
4. Payment Amount vs Fine Amount
    - Overnight Tractor Trailer Fine: \$253
    - Overnight Tractor Trailer Payment: \$157
    - Obstructing Traffic/Intersection Fine: \$115
    - Obstructing Traffic/Intersection Fine: \$109
    - ...
    - Seems like the payment after being fined is always lower for most violations, this could be due to violators fighting the ticket

   

![dashboardFull.JPG](attachment:dashboardFull.JPG)


```python

```
