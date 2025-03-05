# --- Stage 1: Build Stage ---
    FROM node:20-alpine AS builder

    # Set the working directory inside the container
    WORKDIR /app
    
    # Copy package.json and package-lock.json first to leverage caching
    COPY package.json ./
    COPY package-lock.json ./
    
    # Install dependencies
    RUN npm install --only=production
    
    # Copy the rest of the application code
    COPY . .
    
    # --- Stage 2: Runtime Stage ---
    FROM node:20-alpine
    
    # Set the working directory inside the container
    WORKDIR /app
    
    # Copy only the built application from the builder stage
    COPY --from=builder /app /app
    
    # Expose port 3000
    EXPOSE 3000
    
    # Command to run the application
    CMD ["node", "server.js"]