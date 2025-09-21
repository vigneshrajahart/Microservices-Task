# Microservices Containerization with Node.js, Docker & Docker Compose

##  Project Overview

This project demonstrates how to containerize a **microservices-based Node.js application** using **Docker** and orchestrate it using **Docker Compose**.

### Services:

* **User Service** → Port `3000`
* **Product Service** → Port `3001`

* **Gateway Service** → Port `3003`

Each service has its own Dockerfile and will be managed through `docker-compose.yml`.

---

##  Project Structure

```
submission/
├── user-service/
│   └── Dockerfile
├── product-service/
│   └── Dockerfile
├── gateway-service/
│   └── Dockerfile
├── docker-compose.yml
└── README.md
```

---

##  Prerequisites

* Install **Docker Desktop**: [Download here](https://www.docker.com/products/docker-desktop)
* Install **Git**: [Download here](https://git-scm.com/downloads)
* GitHub account for pushing the code

---

## 🛠 Setup Instructions

### 1. Clone the Repository

First, fork the repository given by your instructor. Then clone your fork:

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

### 2. Build and Run Containers

Run the following command in the project root (where `docker-compose.yml` is located):

```bash
docker-compose up --build
```

### 3. Verify Services

Open your browser or use curl to test:

* User Service → [http://localhost:3000](http://localhost:3000)
* Product Service → [http://localhost:3001](http://localhost:3001)
* Order Service →[http://localhost:3002](http://localhost:3002)
* Gateway Service → [http://localhost:3003](http://localhost:3003)

### 4. Stop Containers

```bash
docker-compose down
```

---

## 🔍 Testing the Services

Use curl or browser to test endpoints. Example:

```bash
curl http://localhost:3000/users
curl http://localhost:3001/products
curl http://localhost:3003/order
curl http://localhost:3003/gateway

```

---

##  Troubleshooting

* **Error: Port already in use** → Stop any application using `3000`, `3001`, or `3003`.
* **Containers not building** → Ensure `Dockerfile` exists in each service folder.
* **Service not accessible** → Run `docker ps` and check if all containers are running.

---

##  Push Changes to GitHub

After making changes:

### 1. Check Current Branch

```bash
git branch
```

If you are on `main` or `master`, create a new branch:

```bash
git checkout -b containerization-task
```

### 2. Stage and Commit Changes

```bash
git add .
git commit -m "Added Dockerfiles, docker-compose.yml, and README"
```

### 3. Push Changes

```bash
git push origin containerization-task
```

### 4. Create a Pull Request

1. Go to your GitHub fork.
2. Click **Compare & pull request**.
3. Add a description and submit.

---

## 📸 Screenshots to Include in Submission

* `docker-compose up` showing successful container startup.
* Browser screenshot of each service running.
* Output of `docker ps` showing active containers.


********************* Added All the screenshots in the Word doc ******************************************

---


