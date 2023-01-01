# Setup AKS Kubernetes in Azure

Setup AKS Kubernetes in Azure: 

1. I head to Kubernetes services on Azure. 

![Untitled](https://user-images.githubusercontent.com/42151912/210174471-87a0b1b4-f204-46dd-9562-608b73718c7e.png)


2. I create a cluster with a new resource group called aks-demo, and also the region is uk-south

![Untitled 1](https://user-images.githubusercontent.com/42151912/210174483-feb5b44a-a8af-4f2d-bd71-536481bd8943.png)

![Untitled 2](https://user-images.githubusercontent.com/42151912/210174485-7cad7958-f50c-46f7-b181-2870b7aa95fc.png)

![Untitled 3](https://user-images.githubusercontent.com/42151912/210174490-1c3420c3-f5e3-493d-b2ba-6fb33111d80f.png)


I change the node size to B2’s - which has 2 cpu’s and 4 ram 

I also make the node count range 1-2 

![Untitled 4](https://user-images.githubusercontent.com/42151912/210174500-8a7c0df7-af5f-4685-8f7a-0eb12550d90f.png)

![Untitled 5](https://user-images.githubusercontent.com/42151912/210174508-4b89377f-789d-4d7b-97aa-dce49e638489.png)

![Untitled 6](https://user-images.githubusercontent.com/42151912/210174509-f6eaf06d-fe26-4a05-aec0-dc57078f51a4.png)


On the next page, I leave access, networking, integrations, advanced, tags and review + create. 

![Untitled 7](https://user-images.githubusercontent.com/42151912/210174512-5381e746-7579-45ad-99e4-205e7acad706.png)

![Untitled 8](https://user-images.githubusercontent.com/42151912/210174521-aae0d0fa-4d4d-4c2f-bc88-3a4005d3ec7d.png)

![Untitled 9](https://user-images.githubusercontent.com/42151912/210174526-950d9710-55db-401b-b739-9beec1a76624.png)


I refresh the list and the deployment is in process, I’ll wait usually a couple of minutes before it is done. 

![Untitled 10](https://user-images.githubusercontent.com/42151912/210174533-f06ba269-19d8-4bb7-92ab-bbdf40264a2b.png)

![Untitled 11](https://user-images.githubusercontent.com/42151912/210174542-e0700335-e851-4115-9dac-164df0e379ce.png)

![Untitled 12](https://user-images.githubusercontent.com/42151912/210174545-cc89b211-742f-4a2b-a0be-fbaf8d8c2965.png)


Next I go the service.

![Untitled 13](https://user-images.githubusercontent.com/42151912/210174550-3c59712e-a344-45c7-a7fa-af45615a284d.png)

