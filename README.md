# Hands-on-L3

## Project Description
This project demonstrates a multi-container microservice application using **Python Flask**, **Redis caching**, and **Docker Compose** for orchestration. The application tracks page view counts using Redis and serves them through a Flask web application.

## Directory Structure
-Dockerfile

-README.md

-Submission file.pdf

-app.py

-compose.yaml

-requirements.txt

# **1. Install Docker Desktop (macOS)**
1. Download Docker Desktop for Mac from:
 https://www.docker.com/products/docker-desktop/

3. Open the .dmg file and drag Docker.app into Applications

4. Open Docker.app and follow security prompts

5. Verify installation:
docker --version

## 2. Build and run the application: 

docker compose up

## 3. Open the application in a browser at: 

http://localhost:8000

##  Key Learnings

### **Technical Skills Acquired:**
1. **Docker Mastery**: Container creation, image building, and port management
2. **Multi-Service Orchestration**: Using Docker Compose to coordinate Flask and Redis services
3. **Container Networking**: Establishing communication between independent services
4. **Error Debugging**: Troubleshooting Docker build and runtime issues
5. **Microservice Design**: Implementing loosely coupled, independently scalable services

### app.py

    import time

    import redis

    from flask import Flask

    app = Flask(__name__)

    cache = redis.Redis(host='redis', port=6379)


    def get_hit_count():

    retries = 5
    
    while True:
    
        try:
        
            return cache.incr('hits')
        
        except redis.exceptions.ConnectionError as exc:
        
            if retries == 0:
            
                raise exc
            
            retries -= 1
           
            time.sleep(0.5)



     @app.route('/')

    def hello():

    count = get_hit_count()
    
    return 'Hello World! I have been seen {} times.\n'.format(count)

    if __name__ == '__main__':
        app.run(host='0.0.0.0', port=5000)


<img width="2544" height="1428" alt="Screenshot 2026-02-03 at 5 53 15 PM" src="https://github.com/user-attachments/assets/f9a70307-bc28-4d8a-bbbd-b7e22806d8af" />
<img width="2935" height="1810" alt="Screenshot 2026-02-03 at 5 46 06 PM" src="https://github.com/user-attachments/assets/a15f2871-9de1-4831-8993-3aaa7a3dcd42" />
