# --- Stage 1: Build ---
FROM node:18.20.8-alpine AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy package files first to leverage Docker layer caching
#COPY package*.json ./

# Copy the rest of the application source code
COPY  . .

RUN npm install

#CMD digunakan untuk run command inside container
CMD npm start
