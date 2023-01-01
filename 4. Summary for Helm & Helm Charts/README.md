# Summary for Helm & Helm Charts

### Install and configure Helm in Jenkins Server:

For this Helm/Helm charts project, I first started off by going back to my Jenkins-server tab in my terminal and downloaded the helm script using the curl command. Gave permissions the to the script using chmod.

Made a new directory called ‘.kube’ on my local machine terminal and cd into that new directory. 

I headed back to azure portal and connected the AKS cluster by using the 2 given commands ‘az account set….’ and ‘az aks get-credentials’. 

Once that was done I went into the Azure cloud shell in (bash mode) on azure portal.

Afterwards I go back to the terminal and check if the config file is available in which it was. 

On the azure cloud shell, I open that config file ‘cat config’ and copied all the contents inside that file. Headed back to my local machine’s terminal and made sure I was in the same path as that .kube directory I created earlier. I edit the config file using the vi editor command and pasted those contents from the other config file earlier that is on the AKS cluster. 

I ran ‘helm list’ and saw an error that the config file was group-readable, to change that I needed to give permissions to that config file by running ‘chmod 600’ and then I ran ‘helm list’ again and got no errors. 

