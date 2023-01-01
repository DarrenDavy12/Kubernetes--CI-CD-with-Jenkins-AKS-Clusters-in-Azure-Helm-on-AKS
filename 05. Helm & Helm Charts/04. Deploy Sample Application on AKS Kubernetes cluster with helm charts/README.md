# Deploy Sample Application on AKS Kubernetes cluster with helm charts

Deploy Sample Application on AKS Kubernetes cluster with helm charts:

1. I install the myqsl 1.6.9 with helm by running `helm install mysqldb mysql-1.6.9.tgz`

![Untitled](https://user-images.githubusercontent.com/42151912/210176505-bff7c81c-dd5a-4c1b-a473-8df17087289f.png)

2. Next I run `helm list` and see the chart.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9886de7b-a687-4d1d-9492-054dea995e4a/Untitled.png)

1. Then I run `kubectl get pods` in another tab on the terminal under `/users/<user_name>` to see the status of the pods. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79722b08-971e-4f1e-9e8e-4c75142f77f1/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/074ba634-e61d-4781-a718-4cc8113d9270/Untitled.png)

1. `kubectl get svc` to check the service.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6325fc25-d8e9-41e7-8482-888ce8a8f754/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ec77a69-93a9-4428-9346-1ec09341c046/Untitled.png)

1. `kubectl get pvc` for the physical volume. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/24415fce-452f-4383-a2c8-79a6ce09c737/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b43ba21-f72d-4d28-bd3d-29d00ef84037/Untitled.png)

Now I choose any helm chart for the Kubernetes cluster, the helm chart Im going to use is supported by nginx so I return back to my tab open live with the jenkins-server, go to `cd mysql/templates/`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3d039d91-86e5-484f-bbc8-856136a83bf8/Untitled.png)

I next run `helm search repo stable/nginx` and it should be available.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/03f54d1e-4d38-4b04-9621-81a85b16d785/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63293914-b5d5-4a07-8fd2-d8399994789f/Untitled.png)

Afterwards, I delete the release for mysqldb, first I run `helm list` and then `helm uninstall mysqldb` 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/20fdbe3a-8e7a-460b-884e-d6dc0b3dcb94/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0263f939-cba5-41f3-8526-51467b67bede/Untitled.png)

I check in my local machine terminal and run `kubectl get pods` and should see no resources. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/411c552c-6a56-4eb6-a15b-5037012a9a3d/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5eaa0767-f9ba-4f1b-b232-86918e8c9834/Untitled.png)

Back in the jenkins-server I run `helm install nginx-test stable/nginx-ingress` after I run `helm list` 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/07dee1a1-9455-41b6-9eba-64d95b4febc4/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/141fbd7c-db7a-410f-a79f-0568249bfff1/Untitled.png)

On local terminal I run `kubectl get pods` again to see deployed apps.
