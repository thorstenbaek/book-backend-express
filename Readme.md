# Installations 

## Create K8S Cluster
https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli


Create Resourcegroup
az group create --name tstResourceGroup --location norwayeast

Create AKS Cluster
az aks create -g tstResourceGroup -n tstAKSCluster --enable-managed-identity --node-count 1 --enable-addons monitoring --enable-msi-auth-for-monitoring  --generate-ssh-keys

Connect CLI to Cluster
az aks get-credentials --resource-group tstResourceGroup --name tstAKSCluster

## ngress-nginx-controller
https://learn.microsoft.com/en-us/azure/aks/ingress-basic?tabs=azure-cli

helm install ingress-nginx ingress-nginx/ingress-nginx --create-namespace --namespace ingress-nginx --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz

## cert-manager
https://cert-manager.io/docs/tutorials/acme/nginx-ingress/
https://cert-manager.io/docs/installation/helm/

helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.11.0 --set installCRDs=true

# Create Azure Blob Store

https://learn.microsoft.com/en-us/azure/event-grid/storage-upload-process-images?tabs=dotnet%2Cazure-powershell

## Create Resource Group
New-AzResourceGroup -Name imagesResourceGroup -Location WestEurope

## Create StorageAccount
New-AzStorageAccount -ResourceGroupName imagesResourceGroup -Name bookimagesstorageaccount -SkuName Standard_LRS -Location westeurope -Kind StorageV2 -AccessTier Hot

Har kommet frem til å opprette Containers (Folders) - se i nettsiden...