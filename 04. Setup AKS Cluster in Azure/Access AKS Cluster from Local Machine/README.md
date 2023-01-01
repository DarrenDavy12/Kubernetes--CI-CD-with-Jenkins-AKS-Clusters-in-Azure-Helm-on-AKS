# Access AKS Cluster from Local Machine

I download Azure CLI with homebrew with `brew install azure-cli` 

Once the download is complete, I install the .msi file to get azure cli. 

I open another tab in my terminal and I type `az` and hit enter to test whether Azure CLI is installed correctly or not. 

If not, I download Azure CLI with homebrew with `brew install azure-cli` and once installed, I run `az upgrade` 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fcdab4dc-e7da-4a91-8815-9a535e9cdaa2/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bcc96bc4-b6c4-4e75-b4d3-fdc8e657a91e/Untitled.png)

Once installation is completed, need to access azure with below commands:

`az login`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/320e0120-4e75-4f65-a855-c49666a97283/Untitled.png)

I run `az account set -s <id>` to set the account. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3acb89a6-6b67-4566-bc0c-c30a03755c7a/Untitled.png)

Then `az aks get-credentials --resource-group=<RGNAME> --name=<AKSCLUSTERNAME>`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e431464-f288-421f-8a82-d669e2e09cef/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b405abc4-575e-4b9a-b95a-db8ac11be326/Untitled.png)

Next I install kubectl by running `curl -LO "https://dl.k8s.io/release/**$(**
curl -L -s https://dl.k8s.io/release/stable.txt**)**
/bin/darwin/amd64/kubectl"`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56d956c7-8ddb-4751-986f-01543596e1a6/Untitled.png)

I list the pods using `kubectl get pods -n kube-system`
