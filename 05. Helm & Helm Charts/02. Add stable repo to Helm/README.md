# Add stable repo to Helm

1. I run `helm repo add stable [https://charts.helm.sh/stable](https://charts.helm.sh/stable)` to get the stable repository.

![Untitled](https://user-images.githubusercontent.com/42151912/210176264-611bd569-95c1-4c78-bab6-a91978264d18.png)


2. Then I run `helm repo list` and see the added repo. 

![Untitled 1](https://user-images.githubusercontent.com/42151912/210176271-3f78a6a4-3050-4559-ad66-a3032d8a3b3a.png)


3. Next I run `helm search repo stable` , this command will give me the output of all the helm charts available inside the stable repository. I will use the fluent-bit chart for an example if I run `helm search repo stable/fluent-bit` it will show me this.

![Untitled 2](https://user-images.githubusercontent.com/42151912/210176312-07f7451a-70c1-4a5a-8b90-920643910688.png)

![Untitled 3](https://user-images.githubusercontent.com/42151912/210176317-c564ab64-3d0d-482e-a52e-b890e252535c.png)
