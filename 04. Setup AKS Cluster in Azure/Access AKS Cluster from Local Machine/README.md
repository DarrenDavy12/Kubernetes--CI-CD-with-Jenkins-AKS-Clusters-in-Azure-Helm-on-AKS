# Access AKS Cluster from Local Machine

I download Azure CLI with homebrew with `brew install azure-cli` 

Once the download is complete, I install the .msi file to get azure cli. 

I open another tab in my terminal and I type `az` and hit enter to test whether Azure CLI is installed correctly or not. 


If not, I download Azure CLI with homebrew with `brew install azure-cli` and once installed, I run `az upgrade` 

![Untitled](https://user-images.githubusercontent.com/42151912/210174722-927a1ede-2f61-46ed-a55b-729240ddbc49.png)

![Untitled 1](https://user-images.githubusercontent.com/42151912/210174727-0d8ad84e-23ec-4ea9-82d3-fda8ef6f0813.png)


Once installation is completed, need to access azure with below commands:

`az login`

![Untitled 2](https://user-images.githubusercontent.com/42151912/210174738-3a5f0e9c-5972-4d49-8010-f2605549a65f.png)


I run `az account set -s <id>` to set the account. 

![Untitled 3](https://user-images.githubusercontent.com/42151912/210174742-2263521c-b087-4ba8-9e60-c791acf03adb.png)


Then `az aks get-credentials --resource-group=<RGNAME> --name=<AKSCLUSTERNAME>`

![Untitled 4](https://user-images.githubusercontent.com/42151912/210174750-31475f04-86d7-49c4-b147-3af4c264f2ea.png)

![Untitled 5](https://user-images.githubusercontent.com/42151912/210174759-62be3eeb-dadb-45a8-a5c1-bc782e7a380b.png)


Next I install kubectl by running `curl -LO "https://dl.k8s.io/release/**$(**
curl -L -s https://dl.k8s.io/release/stable.txt**)**
/bin/darwin/amd64/kubectl"`

![Untitled 6](https://user-images.githubusercontent.com/42151912/210174765-95dc0619-598e-4c66-bf3f-72b1f518ca96.png)

I list the pods using `kubectl get pods -n kube-system`

![Untitled 7](https://user-images.githubusercontent.com/42151912/210174788-caaa1fef-3f35-4456-9750-50db70353f4f.png)
