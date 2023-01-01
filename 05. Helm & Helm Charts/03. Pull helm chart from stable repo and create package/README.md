# Pull helm chart from stable repo and create package

Pull helm chart from stable repo and create package:

1. I run `helm search repo stable/mysql` 

![Untitled](https://user-images.githubusercontent.com/42151912/210176397-32870adf-fdab-4a98-a23e-67d7352966d0.png)

2. Then `helm pull stable/mysql` to pull the mysql chart, `ls -ltr` to see the package.

![Untitled 1](https://user-images.githubusercontent.com/42151912/210176406-050ddf27-5faa-410d-9699-a998ebb30d37.png)

3. Then I extract the zip file by running `tar -xvzf <zip_file>`

![Untitled 2](https://user-images.githubusercontent.com/42151912/210176412-a35ade64-130c-48bf-bb09-441934836918.png)


4. I cd into the newly extracted directory and run `ls -ltr` and I see a templates folder and `cd` into that.

![Untitled 3](https://user-images.githubusercontent.com/42151912/210176419-96ee7d33-a249-41c2-babe-90fddf4b18f3.png)

![Untitled 4](https://user-images.githubusercontent.com/42151912/210176423-1dcc744d-4aae-4d04-be23-770cd7799b87.png)

![Untitled 5](https://user-images.githubusercontent.com/42151912/210176426-9b8d5b10-cf16-4a49-b07a-945621b542fe.png)


5. I `cd..` to get back to the path `/var/lib/jenkins/mysql` I can see chart.yaml.

![Untitled 6](https://user-images.githubusercontent.com/42151912/210176432-2bb47707-63be-423e-b1b3-963b68def05e.png)

6. Next I edit that chart.yaml file `vi Chart.yaml` and change the version at the bottom to `1.7.0` , after that I save and quit.

![Untitled 7](https://user-images.githubusercontent.com/42151912/210176437-3fe6b438-a71a-4719-ad5b-8c6980fa047d.png)

7. I head back to the Jenkins directory `cd /var/lib/jenkins` 

![Untitled 8](https://user-images.githubusercontent.com/42151912/210176444-ca8ff758-d472-46f2-9fd4-6fa8c831fc7c.png)

8. Next I run `helm package mysql` to create the package.

![Untitled 9](https://user-images.githubusercontent.com/42151912/210176447-80dbc9c0-89a9-46eb-bc39-f4c84ade2162.png)

