# Docker Demo Experiment 
This is the demo docker
# Docker Build Demo

A simple Node.js application demonstrating Docker image building and containerization.

## Project Structure
```
.
├── server.js          
├── package.json      
├── Dockerfile         
├── .dockerignore      
└── README.md          
```
## Prerequisites

- Docker installed on your system
- Basic knowledge of command line
 
## Building the Docker Image

### Basic Build

Build the image with a tag:

```bash
docker build -t my-node-app .
```

### Build with Custom Tag

```bash
docker build -t my-node-app:v1.0.0 .
```

### Build with No Cache

```bash
docker build --no-cache -t my-node-app .
```

## Running the Container

### Basic Run

```bash
docker run -p 3000:3000 my-node-app
```

### Run in Detached Mode

```bash
docker run -d -p 3000:3000 --name my-app my-node-app
```

### Run with Environment Variables

```bash
docker run -p 3000:3000 -e NODE_ENV=production -e PORT=3000 my-node-app
```

## Testing the Application

Once the container is running, test it with:

```bash
# Main endpoint
curl http://localhost:3000

# Health check endpoint
curl http://localhost:3000/health
```

## Useful Docker Commands

### List Images

```bash
docker images
```

### List Running Containers

```bash
docker ps
```

### List All Containers

```bash
docker ps -a
```

### Stop Container

```bash
docker stop my-app
```

### Remove Container

```bash
docker rm my-app
```

### Remove Image

```bash
docker rmi my-node-app
```

### View Container Logs

```bash
docker logs my-app
```

### Execute Commands in Running Container

```bash
docker exec -it my-app sh
```

## Advanced: Multi-stage Build Example

To optimize the image size, you could use a multi-stage build:

```dockerfile
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install

# Production stage
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

## Troubleshooting

- **Port already in use**: Change the host port: `docker run -p 8080:3000 my-node-app`
- **Build fails**: Ensure Docker daemon is running: `docker info`
- **Permission denied**: On Linux, you may need to use `sudo` or add your user to the docker group
