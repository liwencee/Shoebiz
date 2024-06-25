# Shoebiz

This project is to dockerize a code base and deploy on docker hub. this dockerfile is downloaded and deoploy into kubernetes and later the website is deployed on the brouser

STEPS 
**************************************************************

Create a project Dirextory
Inside the directory create HTML (index.html) and CSS Files
Initialize Git repository into thr project directory
Add and commit your git codes into your Github

DOCKERIZE THE APPLICATION
Create a dockerfile specifing Nginx as the Base file..
paste the html and css code into the dockerfile file directory
type Docker build -t nameserverNginx .
tag the nginx image "docker tag shoewebserver/nginx lehqan/shoewebserver"
login to docker hub from your terminal
then push the image to docker hub "docker push lehqan/shoewebserver:latest"

DEPLOY TO KUBERNETES
******************************************************************

Install kind (kubernetes in docker)
Create a kind cluster

apiVersion: apps/v1
kind: Deployment
metadata:
  name: weather-service
spec:
  replicas: 3
  selector:
    matchLabels:
      app: weather-service
  template:
    metadata:
      labels:
        app: weather-service
    spec:
      containers:
      - name: weather-service
        image: your-dockerhub-username/weather-service:latest
        ports:
        - containerPort: 80

DEPLOY TO KUBERNETES
**************************************************************************

Create a kubernete deployment YAML file specifying the type as image and desired replicas
Apply the deployment to your cluster

kubectl apply -f weather-service-deployment.yaml

CREATE A SERVICE(CluaterIP)
**************************************************************************
Create a kubernetes Services YAML file specifying the type as clusterIP
Apply the service to your cluster.

apiVersion: v1
kind: Service
metadata:
  name: weather-service
spec:
  selector:
    app: weather-service
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP

  kubectl apply -f weather-service-service.yaml

  kubectl port-forward service/weather-service 8080:80

  
ACCESS THE APPLICATION
Port-forward to the service to access the application locally
Open your brouser and visit the specified port to view your simple frontend application






