# Coin Price Monitoring Project 
This repository contains cloud computing course final project at Amirkabir University of Technology. 

## Step 1: Application Development

The Coin Price Monitoring project is aimed at creating a cryptocurrency price monitoring application. This application comprises a database and two services: "bepa" and "peyk."

### Bepa Service
The bepa service is responsible for retrieving the latest cryptocurrency prices and storing them in the database. It operates periodically at specified intervals. The bepa service accomplishes two key tasks:

1. **Data Retrieval**: It requests the latest prices from the coinnews API to retrieve the most recent values. After receiving the response, it writes the results to the Prices table in the database. The API provides endpoints for getting a list of active coins, retrieving the price of each coin, and accessing price history. You should run this service on your cluster using the provided data files.

2. **Alerts**: To send alerts to users, bepa calculates the percentage change in the price of each cryptocurrency compared to the last recorded price in the table. It then checks the Alert Subscriptions table to identify triggered alerts and informs users by sending email notifications. You can use Mailgun or another email service for sending emails.

### Peyk Service
The Peyk service offers two endpoints for users:

1. **SubscribeCoin**: Users can subscribe to price changes of a desired cryptocurrency by providing their email, cryptocurrency name, and desired percentage change.

2. **GetPriceHistory**: This endpoint returns the price history of a cryptocurrency when users send a request containing the cryptocurrency name.

You have flexibility in implementing the request and response data formats for these endpoints.

## Step 2: Containerization

After developing the two services, you should containerize each one using Docker and write a Dockerfile to build a Docker image. Employ the multi-stage builds technique to generate images in two stages, where the first stage builds the project and generates an executable file, and the second stage runs this file in an Alpine container. This technique is applicable to both compiled and interpreted languages.

## Step 3: Deploying the Application with Kubernetes

In this step, we deploy the containers using Kubernetes. Various components of the project, including the database, bepa service, and peyk service, require specific resources to run on Kubernetes.

### bepa Service
- bepa runs as a Kubernetes CronJob, periodically executing the image built in the previous step every 3 minutes.

### peyk Service
- A deployment runs the peyk server in two pods. This deployment should have access to the configmap and secret content so that its pods can use this information to access the database, etc.
- A service is created to facilitate communication with the peyk service pods.

The Kubernetes resources mentioned here should be created in logical dependency order, from right to left and top to bottom, using the `kubectl apply` command.

## Final Step: Extra Credit (Docker Compose)

Docker compose deployed for project.

