# Setup Jenkins in AKS Cluster for CI/CD

Installing Jenkins Server for CI/CD to AKS Kubernetes Cluster:

1. First, connected to the Azure Portal [https://portal.azure.com/#home](https://portal.azure.com/#home) and search for Virtual Machines 

![Untitled](https://user-images.githubusercontent.com/42151912/210168483-30ed4f4c-cc75-44b3-a00d-a83bbab00746.png)

![Untitled 1](https://user-images.githubusercontent.com/42151912/210168544-9c0cf4d8-0c6b-4e76-ae4c-2d00e83f3f7e.png)


2. I created a new resource group and call it ‘jenkins’

![Untitled 2](https://user-images.githubusercontent.com/42151912/210168548-b0864ebb-45c1-4078-8a00-08b0c3a316ab.png)


3. Provide Virtual Machine name, the region, I selected CentOS as the image, I choose Standard_B2’s because the application thats going to have maven it expects 2 cpu’s and 4 GB of ram. 

![Untitled 3](https://user-images.githubusercontent.com/42151912/210168554-447c26b7-1a04-4b53-9f45-1b53c9cc8b80.png)


4. I select password as the authentication type and create a username and password for the admin account. Afterwards I press ‘Next:Disks’ 

![Untitled 4](https://user-images.githubusercontent.com/42151912/210168563-2e18d519-131f-4b7a-a59c-cfe8f581c75f.png)


5. I use Standard SSD as the OS disk type, leave everything else default and click ‘Next:Networking’ 

![Untitled 5](https://user-images.githubusercontent.com/42151912/210168570-e47099fe-6fba-4b6d-a010-54c8289a792d.png)


I leave Networking page as default, leave advanced and tags page on default too and click Review+Create. Wait for validation and click Create. 

![Untitled 6](https://user-images.githubusercontent.com/42151912/210168588-87f62ee8-9691-46cf-9698-d26f6fed5f4d.png)


Go to resource and copy the public IP address shown. 

![Untitled 7](https://user-images.githubusercontent.com/42151912/210168599-01a562ed-b52c-4b1b-b0bd-e4ccec597e59.png)

![Untitled 8](https://user-images.githubusercontent.com/42151912/210168615-5cbac922-0ba5-4487-85dd-8fb41b2a282e.png)


6. In the top search bar, I search SSH Keys and create a SSH Key pair.

![Untitled 9](https://user-images.githubusercontent.com/42151912/210168617-750e4014-f07d-462c-8b3e-d567a5e43eec.png)

![Untitled 10](https://user-images.githubusercontent.com/42151912/210168621-65b7d2fe-970f-4cd1-a662-b7bea7246b20.png)


I fill out the details. After I click Review+Create.

![Untitled 11](https://user-images.githubusercontent.com/42151912/210168627-c8cfa830-1ee6-40c3-8f33-53ce85148467.png)


Then I click Create.

![Untitled 12](https://user-images.githubusercontent.com/42151912/210168632-3d6434f9-c8ff-4ea4-b7e6-692427c04337.png)


Once created I select download key and put the `.pem` key inside my keys folder on my local machine. 

![Untitled 13](https://user-images.githubusercontent.com/42151912/210168636-b8dab407-2e56-4c01-83fd-97f1122d8164.png)


I run in the terminal inside my key directory - `chmod 400 <key_pair>.pem`

![Untitled 14](https://user-images.githubusercontent.com/42151912/210168642-a228684a-35dc-41e9-9175-5398e5a36de6.png)


Then I ssh into the server by running `ssh -i <key_name>.pem <adminName>@<publicIP>`

![Untitled 15](https://user-images.githubusercontent.com/42151912/210168649-f8c69fde-6a9c-4cc9-a465-561061c7f060.png)


7. I become root user `sudo su -` , now I run `yum install jenkins` 

![Untitled 16](https://user-images.githubusercontent.com/42151912/210168654-b5383526-d6f2-400b-8d3b-04aa203cbda1.png)


The default repository inside CentOS does not have the Jenkins software. 

![Untitled 17](https://user-images.githubusercontent.com/42151912/210168658-3b5b2079-73a3-489c-9095-0c546aa7eaca.png)


So I run `cd /etc/yum.repos.d/` 

![Untitled 18](https://user-images.githubusercontent.com/42151912/210168665-039addbc-4c10-4fc1-ae58-7dcd984b53be.png)


I list out the default repos using `ls -ltra`

![Untitled 19](https://user-images.githubusercontent.com/42151912/210168666-ed8230e6-2cb9-4028-bd36-f03bad0a6956.png)


Now I install java to the server using `yum install java-1.8*` and wait till the installation is complete.

![Untitled 20](https://user-images.githubusercontent.com/42151912/210168671-098f16ad-656b-483e-8518-934232d9c574.png)

![Untitled 21](https://user-images.githubusercontent.com/42151912/210168695-fe296577-2531-452b-9c59-ec63e5c22726.png)

![Untitled 22](https://user-images.githubusercontent.com/42151912/210168698-005a2d26-29d9-4d2f-af8a-8e2c6f69408a.png)


8. Then I run `find /usr/lib/jvm/java-1.8* | head -n 3`

![Untitled 23](https://user-images.githubusercontent.com/42151912/210168705-358e151d-fc69-4efd-8cd4-f49b6b640233.png)


This is directory we use as the JAVA_HOME
`/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.332.b09-1.el7_9.x86_64`

![Untitled 24](https://user-images.githubusercontent.com/42151912/210168707-82f26a08-136d-4b28-80c0-c0655d4078d3.png)


9. I ran `cd` and then `vi .bash_profile` to open the file, add the JAVA_HOME path and export JAVA_HOME. 

File should look like this. 

![Untitled 25](https://user-images.githubusercontent.com/42151912/210168752-2b290525-aeb2-4175-81c7-9a590591776b.png)


10. Then I execute this command to update the bash_profile-  `source ~/.bash_profile`

![Untitled 26](https://user-images.githubusercontent.com/42151912/210168760-daeb7861-bcdb-4793-8275-15dcc6dce3f0.png)


11. Ran `yum install wget` to install wget. CentOs already has wget installed by default. 

![Untitled 27](https://user-images.githubusercontent.com/42151912/210168767-04449c63-f3d0-4f26-8ab7-301fd7c05be5.png)


Now I run `wget -O /etc/yum.repos.d/jenkins.repo [https://pkg.jenkins.io/redhat-stable/jenkins.repo](https://pkg.jenkins.io/redhat-stable/jenkins.repo)` to download the Jenkins repo. 

![Untitled 28](https://user-images.githubusercontent.com/42151912/210168770-17230ed6-26b3-4b4f-a4b8-60203097e9aa.png)


Then I import the key `rpm --import [https://pkg.jenkins.io/redhat-stable/jenkins.io.key](https://pkg.jenkins.io/redhat-stable/jenkins.io.key)`

![Untitled 29](https://user-images.githubusercontent.com/42151912/210168771-8c681dc4-d542-49e9-9c14-f2c3b9eee1a1.png)


Now I can run `yum install jenkins` because the it will connect to the repository I downloaded.

![Untitled 30](https://user-images.githubusercontent.com/42151912/210168775-26d8ba09-9d65-4f07-a5c9-fc8d5ed2fae2.png)

![Untitled 31](https://user-images.githubusercontent.com/42151912/210168779-801af654-9de0-43c6-8fe0-db147619aeb2.png)

![Untitled 32](https://user-images.githubusercontent.com/42151912/210168785-f7e9d3cd-6680-4d8f-96ea-5c59d5e6823c.png)


12. Next I run `systemctl start jenkins` to get Jenkins started.

![Untitled 33](https://user-images.githubusercontent.com/42151912/210168787-22018815-7fcb-40ef-a943-30ea915cd464.png)


Then Jenkins to start at boot. `systemctl enable jenkins`

![Untitled 34](https://user-images.githubusercontent.com/42151912/210168794-ca7b07ae-9201-46cd-ae90-e7be0310386b.png)


I can access Jenkins with the Public IP along with port 8080 in the browser. 

But first I need to setup a security group using Azure. I head to Networking. 

![Untitled 35](https://user-images.githubusercontent.com/42151912/210168795-f429e90a-76ca-489f-a4df-8eb071c22311.png)


I click jenkins nsg and select inbound security rules and add a rule.

![Untitled 36](https://user-images.githubusercontent.com/42151912/210168848-65d30dba-bd55-4828-802e-f608945d743c.png)

![Untitled 37](https://user-images.githubusercontent.com/42151912/210168852-3b9b41b1-5ca5-4537-8f88-c77e08422d08.png)

![Untitled 38](https://user-images.githubusercontent.com/42151912/210168853-48d0640e-7400-4df3-b2fd-febd52bc69e5.png)


I make sure the destination port ranges is set to 8080 and click Add.

![Untitled 39](https://user-images.githubusercontent.com/42151912/210168859-b84f18a7-c139-4660-824f-01544c3ee8fe.png)

![Untitled 40](https://user-images.githubusercontent.com/42151912/210168892-d7bb00b8-18a2-40be-83f1-430e5cfdcb59.png)


I go back to the tab using port 8080 and refresh the page and the Jenkins login page has loaded. 

![Untitled 41](https://user-images.githubusercontent.com/42151912/210171596-46ebe338-589d-41f7-b38f-63e37d530320.png)


I run `cat /var/lib/jenkins/secrets/initialAdminPassword` in the terminal to get the initialPassword, copy and paste it below 

![Untitled 42](https://user-images.githubusercontent.com/42151912/210171601-f534ec76-218f-4c7a-b1ea-41ef2dfe7362.png)

![Untitled 44](https://user-images.githubusercontent.com/42151912/210171610-e60ecaee-34e4-45ff-a03a-58be13d16367.png)


I click Install suggested plugins and wait until the plugins have been installed.

![Untitled 45](https://user-images.githubusercontent.com/42151912/210171614-0f1a2943-2a9e-4ad7-86a1-a01b6887c5d8.png)

![Untitled 46](https://user-images.githubusercontent.com/42151912/210171627-7562e707-2de3-41ad-9e92-2f75d53e3a5d.png)



Full in detail for the admin user and click Save and Continue. 

![Untitled 47](https://user-images.githubusercontent.com/42151912/210171635-7e011724-2e86-4519-8105-596775f984fd.png)


I click Save and Finish.

![Untitled 48](https://user-images.githubusercontent.com/42151912/210171640-60a06931-b3d7-41cc-90f5-85532d8b1916.png)


Maven & GIT setup in Jenkins Server:

13. In the terminal, I `cd /opt/` and then I run `wget [https://archive.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz](https://archive.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz)`

![Untitled 49](https://user-images.githubusercontent.com/42151912/210171645-f6d42d8d-8987-4a44-b17f-f06130059058.png)



I then run `ls-ltra` and see maven download. 

![Untitled 50](https://user-images.githubusercontent.com/42151912/210171717-0f862a30-f853-4d12-a960-cfd55ef289cc.png)


After I run `tar -zxvf apache-maven-3.6.0-bin.tar.gz` 

![Untitled 51](https://user-images.githubusercontent.com/42151912/210171727-544b1002-c53c-4e5a-8fe4-33a573990d40.png)


I run `ls-ltra` again and see that at the bottom the download has been unzipped. 

![Untitled 52](https://user-images.githubusercontent.com/42151912/210171735-d1e21f80-5b81-4d8b-b285-7a887cd18e7f.png)


Afterwards, deleted the download by running `rm -rf apache-maven-3.6.0-bin.tar.gz`

![Untitled 53](https://user-images.githubusercontent.com/42151912/210171770-3d5260eb-4a99-4b78-929b-466bd037ae17.png)


Now I will go through the process of installing `mvn` , first I run `cd root/` to enter the root directory and edit the bash_profile running `vi .bash_profile`, I export Maven and give the path, also added the maven variable to the home /bin/ path. 
Then I save and quit.

![Untitled 54](https://user-images.githubusercontent.com/42151912/210171777-a7d04952-0028-464d-8fdf-5069c34adc88.png)

![Untitled 55](https://user-images.githubusercontent.com/42151912/210171788-5a6864e0-c14c-46ee-a6d9-b4b840ffc3af.png)


Then I refresh the file with the source command `source ~/.bash_profile` and after run `mvn`

![Untitled 56](https://user-images.githubusercontent.com/42151912/210171796-fd2aae94-2cde-4f82-9a2a-6635c0a9c99d.png)

![Untitled 57](https://user-images.githubusercontent.com/42151912/210171806-3f0a8f4f-c202-40ae-93c3-a40e2f8edb7c.png)



Next I install git running `yum install git` 

![Untitled 58](https://user-images.githubusercontent.com/42151912/210171811-e0eb518d-2d52-45ba-b95d-2e18fe058b1e.png)

![Untitled 59](https://user-images.githubusercontent.com/42151912/210171819-e4d4e721-cdac-4353-9344-73bb51b45786.png)


Docker setup in Jenkins Server: 

14. First I make sure I’m still connected to the Jenkins Server on the browser and then I head back to my terminal by running `yum install docker` and wait till the installation is done.

![Untitled 60](https://user-images.githubusercontent.com/42151912/210171830-a7d2971d-5f10-4655-aa1f-437627a3387e.png)


15. I run `systemctl start docker` to start the docker software.

![Untitled 61](https://user-images.githubusercontent.com/42151912/210171839-7e8af48f-5936-4c79-94cf-2bc6faf74173.png)


16. Then `systemctl enable docker` 

![Untitled 62](https://user-images.githubusercontent.com/42151912/210171845-1f1ddad2-1061-4c67-89d3-bcd747e69bc5.png)


17. I provide permissions to Jenkins user in Jenkins server to access docker using `sudo groupadd docker`

![Untitled 63](https://user-images.githubusercontent.com/42151912/210171849-bac677a4-9f0d-4c5e-a978-0c7639c5cd92.png)


Then I run `sudo usermod -aG docker jenkins` to add the user account. 

![Untitled 64](https://user-images.githubusercontent.com/42151912/210171856-91e4e0f5-d85e-4457-8b1d-f6b7761be65a.png)


Afterwards, I provide permission on this file. `sudo chmod 777 /var/run/docker.sock`

![Untitled 65](https://user-images.githubusercontent.com/42151912/210171963-a66d92ae-201e-4f4f-a0b6-e7adaa8dd893.png)


18. I run `vi /etc/passwd` and edit the automation server to bash not false.

![Untitled 66](https://user-images.githubusercontent.com/42151912/210171971-a1a24ef6-249d-4239-bb90-8bc4111d382e.png)


After that I run `su - jenkins` to login as the Jenkins user. After I run a `id` to see what is install within Jenkins. 

![Untitled 67](https://user-images.githubusercontent.com/42151912/210171974-bf994b5a-4ca2-4d40-8936-b29d70c38ef4.png)


I `exit` out the Jenkins user and then add Jenkins user into sudoers file to get sudo access by running `vi /etc/sudoers` to open file.

![Untitled 68](https://user-images.githubusercontent.com/42151912/210171980-44048e6b-d65e-4e95-84b2-86dd94ee6ff7.png)


I head all the way down to ‘Allow root to run any commands anywhere’ and under the root command I put `jenkins ALL=(ALL) NOPASSWD: ALL`

![Untitled 69](https://user-images.githubusercontent.com/42151912/210171988-06251d97-f9a5-443c-860d-2d980db482ac.png)


Install and configure Docker & Maven plugin in Jenkins server:

19. I head over to the Jenkins server on my browser and go to manage Jenkins. I search for maven and docker.

![Untitled 70](https://user-images.githubusercontent.com/42151912/210172002-23cc87a4-210d-440e-811d-9b387cfe15a2.png)

![Untitled 71](https://user-images.githubusercontent.com/42151912/210172009-fa7f98ce-dfd9-4cc6-bc4a-8fff7d656696.png)


And I tick each plugin and select install without restart and after installation I pick restart Jenkins with no jobs running.

![Untitled 72](https://user-images.githubusercontent.com/42151912/210172019-4651605b-9705-444c-8fc6-3d3633dd0791.png)

![Untitled 73](https://user-images.githubusercontent.com/42151912/210172023-a816fe2a-9219-47c0-ac8a-ed92c160d70d.png)

![Untitled 74](https://user-images.githubusercontent.com/42151912/210172029-f4cb69f1-db62-41cd-9253-13275b71c04c.png)
