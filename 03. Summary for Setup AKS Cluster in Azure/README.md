# Summary for Setup AKS Cluster in Azure

### Setup AKS Kubernetes in Azure:

This did not take long as I did was head to Azure portal and search for Kubernetes services. Created a cluster and choose the region in which I want that cluster to be based in.

Configured the cluster to have 2 cpu’s and 4gb of ram, the usual option for performance for any added tools we wish to add later. Made the node count 1-2 maximum. 

I left most of the tags default after that, once done I click review and create and wait until the deployment process is complete. 

### Access AKS Cluster from Local Machine:

I started off in terminal and downloaded azure’s cli with the brew install command. Then once the download was complete I check the if the installation was done and updated the cli once it was installed. 

Next I set my account, and get the aks cluster credentials with the aks get-credentials command. 

Once done, I install the kubernetes command line tool kubectl by running the curl command and finally I ran ‘kubectl get pods -n kube-system’ to see if I could run any kubectl commands and I could. 

### Creation of Azure Container Registry (ACR):

ACR stores docker images, so once I deploy the application, the Kubernetes cluster can pull the images from azure registry. 

First I headed over to Azure portal and search for container apps. 

Inside container apps, I create a new resource called ‘acr-demo’ and left tags and app settings as default, click create and waited until the container was done.
