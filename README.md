# Project-1-Angular-K8S

### 1. Install NodeJs and Angular CLI on Ubuntu 20.04
    a. Install node js
        $ curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash 
        $ source ~/.bashrc
        $ nvm install node
    
    b. Install angular CLI
        $ npm install -g @angular/cli
### 2. Create angular application
    $ ng new angular-project

### 3. Create the Angular project compiled file
    Build the project. It will create dist folder at root folder
    $ ng build

### 4. Create docker file
    # Dockerfile content
    FROM nginx:alpine
    COPY /dist/angular-project /usr/share/nginx/html

### 5. Create and push docker image to docker-hub
    $ docker build . -t <DOCKER_IMAGE_NAME>:<IMAGE_TAG>
    $ docker build . -t frontend-app:0.1
    $ docker tag <LOCAL-IMAGE>:<LOCAL-TAG> pmv1919/<NEW-IMAGE-NAME>:<NEW-TAG>
    $ docker tag frontend-app:0.1 pmv1919/angular-app:1.0
    $ docker login -u <USERNAME> -p <PASSWORD>
    $ docker push pmv1919/angular-app:1.0

### 6. Deploy angular app using yaml file
    $ minikube start --driver docker --cpus 2 --memory 4096
    $ kubectl apply -f deployment.yaml
    $ kubectl apply -f service.yaml

    Browser:
    http://<INTERNAL-IP>:<NODE-PORT>

### 7. Deploy angular app using helm chart
    $ minikube start --driver docker --cpus 2 --memory 4096
    $ helm create <HELM-CHART-NAME>
    $ helm install <RELEASE-NAME> ./<HELM-CHART-PATH>
    
    Browser:
    http://<INTERNAL-IP>:<NODE-PORT>

### 8. Access application on browser
    $ kubectl get nodes -o wide     # http://<INTERNAL-IP>:<NODE-PORT>
    or 
    minikube ip                     # To get node IP


# Troubleshooting
### 1. InvalidImageName, ImagePullBackOff and ErrImagePull
Fix:
    a. provide the proper name for docker image. Check spelling and tag

### 2. 

Microservices:
https://www.youtube.com/watch?v=pIPji3_rYPY