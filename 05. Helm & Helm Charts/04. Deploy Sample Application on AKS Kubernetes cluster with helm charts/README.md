# Deploy Sample Application on AKS Kubernetes cluster with helm charts

Deploy Sample Application on AKS Kubernetes cluster with helm charts:


1. I install the myqsl 1.6.9 with helm by running `helm install mysqldb mysql-1.6.9.tgz`

![Untitled](https://user-images.githubusercontent.com/42151912/210176505-bff7c81c-dd5a-4c1b-a473-8df17087289f.png)


2. Next I run `helm list` and see the chart.

![Untitled 1](https://user-images.githubusercontent.com/42151912/210243108-4dd226cf-079d-496b-b6cb-1c52e7810642.png)


3. Then I run `kubectl get pods` in another tab on the terminal under `/users/<user_name>` to see the status of the pods. 

![Untitled 2](https://user-images.githubusercontent.com/42151912/210243179-732e2167-eae2-4073-9c24-2cfba2997ddb.png)

![Untitled 3](https://user-images.githubusercontent.com/42151912/210243195-b2c13598-3f53-4a12-94a3-ae39b27ffa17.png)


4. `kubectl get svc` to check the service.

![Untitled 4](https://user-images.githubusercontent.com/42151912/210243213-5c0d3f85-b402-47df-b94b-17929c18596d.png)

![Untitled 5](https://user-images.githubusercontent.com/42151912/210243223-61be8b67-a7b4-4e58-babf-edbd3a0907ea.png)


1. `kubectl get pvc` for the physical volume. 

![Untitled 6](https://user-images.githubusercontent.com/42151912/210243246-ddacd65e-0766-4fd4-9202-084dc1a9cf04.png)

![Untitled 7](https://user-images.githubusercontent.com/42151912/210243255-4d6ce3d7-72dd-425d-8b39-4b22fefb95ce.png)


Now I choose any helm chart for the Kubernetes cluster, the helm chart Im going to use is supported by nginx so I return back to my tab open live with the jenkins-server, go to `cd mysql/templates/`

![Untitled 8](https://user-images.githubusercontent.com/42151912/210243280-d02ef066-f294-4cb9-9e88-0889980dac4f.png)


I next run `helm search repo stable/nginx` and it should be available.

![Untitled 9](https://user-images.githubusercontent.com/42151912/210243307-100a73a1-e930-4177-aa7c-e1e9e047c08e.png)

![Untitled 10](https://user-images.githubusercontent.com/42151912/210243330-6ceec9ec-d3e4-4f63-a64d-7b1bbe464cbc.png)


Afterwards, I delete the release for mysqldb, first I run `helm list` and then `helm uninstall mysqldb` 

![Untitled 11](https://user-images.githubusercontent.com/42151912/210243362-218b6836-e73e-4729-9df0-210ee5c6175b.png)

![Untitled 12](https://user-images.githubusercontent.com/42151912/210243378-46dc8881-2d92-4881-beba-dd0a59e065ef.png)


I check in my local machine terminal and run `kubectl get pods` and should see no resources. 

![Untitled 13](https://user-images.githubusercontent.com/42151912/210243401-782cce02-a089-4510-9afe-0e58fb23f68d.png)

![Untitled 14](https://user-images.githubusercontent.com/42151912/210243429-a52accdb-9413-4261-8a68-165a30154007.png)


Back in the jenkins-server I run `helm install nginx-test stable/nginx-ingress` after I run `helm list` 

![Untitled 15](https://user-images.githubusercontent.com/42151912/210243664-2e61625a-9ff4-486b-927d-dbea04cf12c9.png)

![Untitled 16](https://user-images.githubusercontent.com/42151912/210243681-2039dd84-b070-4a6d-a091-4730cb8419c3.png)


On local terminal I run `kubectl get pods` again to see deployed apps.

![Untitled 17](https://user-images.githubusercontent.com/42151912/210243772-f4fe711c-5360-4443-815b-8cf89176b534.png)
