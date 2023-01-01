# Install and configure Helm in Jenkins Server


1. I head back to the tab that has Jenkins server open and ran `id`

![Untitled](https://user-images.githubusercontent.com/42151912/210175325-0ca8d1b5-369a-44e3-b6dd-0822b48c92cc.png)


2. To download and install helm first I run `curl -fsSL -o get_helm.sh [https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3](https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3)`
 
![Untitled 1](https://user-images.githubusercontent.com/42151912/210175341-cf5383c3-2705-4562-b710-9a9f78ef1a0c.png)


3. Then `chmod 777 get_helm.sh`
![Untitled 2](https://user-images.githubusercontent.com/42151912/210175353-49e1735f-3e3e-4b4d-8ebd-0b15396ae615.png)


4. Next I ran `(space) ./get_helm.sh`

![Untitled 3](https://user-images.githubusercontent.com/42151912/210175876-0284e2b0-371d-49b2-b929-1323ea67bea8.png)


5. To check if installed I ran `helm list` 

![Untitled 4](https://user-images.githubusercontent.com/42151912/210175884-876f4a72-29be-45d1-92c7-ccba62640d20.png)


6. I check the path I am in, and make a new directory called .kube 

![Untitled 5](https://user-images.githubusercontent.com/42151912/210175895-e20b9fa3-f0b0-450a-ba78-a40c37fdfd34.png)


7. I change directory into the newly made one. 

![Untitled 6](https://user-images.githubusercontent.com/42151912/210175910-0fab8ff5-867b-46c2-84fd-b9b23d0e4277.png)


8. Back on azure portal, I go to my Kubernetes cluster and click connect and ran the 2 following commands on the right hand side on the cloud shell. After I got up azure cloud shell in (bash mode).

![Untitled 7](https://user-images.githubusercontent.com/42151912/210176100-dbf4260c-4d42-4e42-acb9-1307b71dc3c9.png)

![Untitled 8](https://user-images.githubusercontent.com/42151912/210176111-ab46ebb5-d09b-44e9-939e-f3bf7d73979d.png)


9. I go cd into the the .kube/ ,`cd .kube` directory and list `ls -ltra` the Kubernetes clusters.

![Untitled 9](https://user-images.githubusercontent.com/42151912/210176123-73a3f5a7-65d3-4d74-b070-20c4f54b83ea.png)

![Untitled 10](https://user-images.githubusercontent.com/42151912/210176127-5474dd9a-ea14-4409-8978-52c01d58412b.png)


10. I ran `cat config` and copy all the contents inside that file.
11. 
![Untitled 11](https://user-images.githubusercontent.com/42151912/210176133-cab16fe2-c1e6-4056-8cba-855f86974d81.png)


11. Back on my local machine terminal, I make sure my path is `/var/lib/jenkins/.kube` and ran `vi config` to create new config file and paste those contents I copied in there. 

![Untitled 12](https://user-images.githubusercontent.com/42151912/210176138-b209a19e-7aef-49ad-b80a-0a1234c6f87f.png)

![Untitled 13](https://user-images.githubusercontent.com/42151912/210176146-67b4f5e0-9272-48da-9bb7-3a9f37fb4199.png)

![Untitled 14](https://user-images.githubusercontent.com/42151912/210176150-8aad44be-e961-4edf-b04a-15fab132ee16.png)


12. Next I ran `helm list` and see that the config file is group-readable and I needed to change that with a few commands and was insecure.

![Untitled 15](https://user-images.githubusercontent.com/42151912/210176163-351e8128-2236-4e74-9060-4aa110fbba34.png)


13. I ran `ls -ltr config` 

![Untitled 16](https://user-images.githubusercontent.com/42151912/210176178-97d244a5-8ca8-4dff-b2e0-d3f72ead5399.png)


14. Afterwards I ran `chmod 600 config` 

![Untitled 17](https://user-images.githubusercontent.com/42151912/210176185-ab90d948-abd9-4f25-8156-5eb1cbeb7217.png)


15. Once again I ran `helm list` and I shouldn’t have any errors. 

![Untitled 18](https://user-images.githubusercontent.com/42151912/210176191-4e3b4e73-6a22-4fe7-af91-6853a75dedb8.png)
