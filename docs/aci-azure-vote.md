# ACR login
az acr login --name akstestacr0001

# Build & Push Azure Vote image to ACR
docker build ./src -t akstestacr0001.azurecr.io/azure-vote:0.1
docker push akstestacr0001.azurecr.io/azure-vote:0.1

# Create an container group
az container create -g aks-test -f manifests/aci-azure-vote.yaml

# Get container status
az container show -g aks-test -n azure-vote -o table

# Get container logs
az container logs -g aks-test -n azure-vote --container-name azure-vote-frontend

# Delete container group
az container logs -g aks-test -n azure-vote --container-name azure-vote-frontend