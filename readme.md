NEW FOLDER/
├── frontend/
│   ├── public/
│   │   ├── index.html
│   │   ├── Login.css
│   ├── src/
│   │   ├── components/
│   │   │   └── Login.js
│   │   └── App.js
│   ├── Dockerfile
│   └── package.json
├── backend/
│   ├── app/
│   │   └── main.py
│   ├── requirements.txt
│   └── Dockerfile
├── mysql/
│   ├── db-init.sql
│   └── Dockerfile
├── k8s/
│   ├── frontend-deployment.yaml
│   ├── backend-deployment.yaml
│   └── mysql-deployment.yaml





# From the frontend directory
cd frontend
docker build -t your-dockerhub-username/frontend:latest .
docker push your-dockerhub-username/frontend:latest

# From the backend directory
cd ../backend
docker build -t your-dockerhub-username/backend:latest .
docker push your-dockerhub-username/backend:latest

# From the mysql directory
cd ../mysql
docker build -t your-dockerhub-username/mysql:latest .
docker push your-dockerhub-username/mysql:latest



# Log in to Azure
az login

# Create a resource group
az group create --name myResourceGroup --location eastus

# Create an AKS cluster
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys

# Get the AKS credentials
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster

# Deploy the services
kubectl apply -f k8s/mysql-deployment.yaml
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/frontend-deployment.yaml