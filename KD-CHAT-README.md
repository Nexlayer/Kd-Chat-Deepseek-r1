# Kd-Chat Deepseek-r1

**Kd-Chat Deepseek-r1** is a simple ReactJS-Express application designed to interact with Ollama's Deepseek-r1 1.5b model. This application provides an interface to query and interact with the Deepseek-r1 model, showcasing the integration of a React frontend with an Express backend.

## Description

This project demonstrates how to build a basic chat application using ReactJS for the frontend and Express for the backend. It connects to Ollama's Deepseek-r1 1.5b model to provide responses based on user queries.

## Features

- **ReactJS Frontend**: User interface to send queries and display responses.
- **Express Backend**: Handles requests and interacts with the Deepseek-r1 1.5b model.
- **Ollama Deepseek-r1 Integration**: Connects to the Deepseek-r1 1.5b model for query responses.

## Getting Started

### Prerequisites

- Node.js (version 14 or higher)
- npm (Node Package Manager)
- Docker: Required for containerizing the application

### Installation

1. **Fork and clone the repository**:
   Fork the repository then run the following:
   ```bash
   git clone https://github.com/your-username/Kd-Chat-Deekseek-r1.git
   cd Kd-Chat-Deepseek-r1
   ```
2. **Navigate to frontend and install dependencies**:
   ```bash
   cd kd-chat
   npm install
   ```
3. **Create a build and move to backend directory**:
   ```bash
   npm run build
   mv build ../kd-chat-express
   ```
4. **Build Docker image**:
   ```bash
   docker build -t kd-chat .
   ```
5. **Pull corresponding Ollama Deepseek-r1 image**:
   ```bash
   docker pull katieharris/ollama:deepseek-r1
   ```
6. **Create a network for the containers to connect to and run them**:
   ```bash
   docker network create kd-chat-network
   docker run -d --name ollama --network kd-chat-network katieharris/ollama:deepseek-r1
   docker run -d --name kd-chat -p 3000:3000 --network kd-chat-network -e REACT_APP_API_URL=http://ollama:11434 kd-chat
   ```
