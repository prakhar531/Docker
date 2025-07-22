# Dockerization of Node.js Application

This guide shows how to Dockerize a basic Node.js application with `index.js` as the entry point.

---

## Step 1: Node.js Project Setup

Create a Node.js project with the following structure:

```

.
├── index.js
├── package.json
└── package-lock.json

```

Example `index.js`:

```js
console.log("Hello from Dockerized Node.js App!");
```

---

## Step 2: Dockerfile

Create a file named **Dockerfile** in the project root:

```Dockerfile
FROM ubuntu

# Install dependencies
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get upgrade -y

# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get install -y nodejs

# Copy project files
COPY package.json package.json
COPY package-lock.json package-lock.json
COPY index.js index.js

# Install Node.js dependencies
RUN npm install

# Define entry point
ENTRYPOINT [ "node", "index.js" ]
```

---

## Step 3: Build Docker Image

Use the following command to build the Docker image:

```bash
docker build -t piyush-garg-docker-image .
```

> `-t` specifies the image tag/name, and `.` refers to the Dockerfile's directory.

---

## Step 4: Run Docker Container

Run your image:

```bash
docker run -it -p 8000:8000 piyush-garg-docker-image
```

> `-p` maps port 8000 of the host to the container. `-it` runs it in interactive mode.

---

## Step 5: Publish to Docker Hub

1. **Create a Docker Hub account** at [hub.docker.com](https://hub.docker.com)
2. **Login locally**:

   ```bash
   docker login
   ```

3. **Tag your image** using your Docker Hub username:

   ```bash
   docker tag piyush-garg-docker-image your-username/image-name
   ```

4. **Push to Docker Hub**:

   ```bash
   docker push your-username/image-name
   ```

---

This is how you can push to docker hub
