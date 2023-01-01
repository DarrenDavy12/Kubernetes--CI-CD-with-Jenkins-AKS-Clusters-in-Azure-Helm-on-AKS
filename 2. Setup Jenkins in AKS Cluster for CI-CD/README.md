# Setup Jenkins in AKS Cluster for CI/CD

Installing Jenkins Server for CI/CD to AKS Kubernetes Cluster:

1. Connect to the Azure Portal [https://portal.azure.com/#home](https://portal.azure.com/#home) and search for Virtual Machines 

![Untitled](https://user-images.githubusercontent.com/42151912/210168483-30ed4f4c-cc75-44b3-a00d-a83bbab00746.png)


![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%201.png)

2. I create new resource group and call it ‘jenkins’

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%202.png)

3. Provide Virtual Machine name, the region, I selected CentOS as the image, I choose Standard_B2’s because the application thats going to have maven it expects 2 cpu’s and 4 GB of ram. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%203.png)

4. I select password as the authentication type and create a username and password for the admin account. Afterwards I press ‘Next:Disks’ 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%204.png)

5. I use Standard SSD as the OS disk type, leave everything else default and click ‘Next:Networking’ 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%205.png)

I leave Networking page as default, leave advanced and tags page on default too and click Review+Create. Wait for validation and click Create. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%206.png)

Go to resource and copy the public IP address shown. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%207.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%208.png)

6. In the top search bar, I search SSH Keys and create a SSH Key pair.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%209.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2010.png)

I fill out the details. After I click Review+Create.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2011.png)

Then I click Create.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2012.png)

Once created I select download key and put the `.pem` key inside my keys folder on my local machine. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2013.png)

I run in the terminal inside my key directory - `chmod 400 <key_pair>.pem`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2014.png)

Then I ssh into the server by running `ssh -i <key_name>.pem <adminName>@<publicIP>`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2015.png)

7. I become root user `sudo su -` , now I run `yum install jenkins` 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2016.png)

The default repository inside CentOS does not have the Jenkins software. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2017.png)

So I run `cd /etc/yum.repos.d/` 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2018.png)

I list out the default repos using `ls -ltra`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2019.png)

Now I install java to the server using `yum install java-1.8*` and wait till the installation is complete.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2020.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2021.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2022.png)

8. Then I run `find /usr/lib/jvm/java-1.8* | head -n 3`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2023.png)

This is directory we use as the JAVA_HOME

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2024.png)

`/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.332.b09-1.el7_9.x86_64`

9. I run `cd` and then `vi .bash_profile` to open the file, add the JAVA_HOME path and export JAVA_HOME. 

File should look like this. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2025.png)

10. Then I execute this command to update the bash_profile-  `source ~/.bash_profile`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2026.png)

11. I run `yum install wget` to install wget. CentOs already has wget installed by default. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2027.png)

Now I run `wget -O /etc/yum.repos.d/jenkins.repo [https://pkg.jenkins.io/redhat-stable/jenkins.repo](https://pkg.jenkins.io/redhat-stable/jenkins.repo)` to download the Jenkins repo. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2028.png)

Then I import the key `rpm --import [https://pkg.jenkins.io/redhat-stable/jenkins.io.key](https://pkg.jenkins.io/redhat-stable/jenkins.io.key)`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2029.png)

Now I can run `yum install jenkins` because the it will connect to the repository I downloaded.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2030.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2031.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2032.png)

12. Next I run `systemctl start jenkins` to get Jenkins started.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2033.png)

Then Jenkins to start at boot. `systemctl enable jenkins`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2034.png)

Now I can access Jenkins with the Public IP along with port 8080 in the browser. 

But first I need to setup a security group using Azure. I head to Networking. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2035.png)

I click jenkins nsg and select inbound security rules and add a rule.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2036.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2037.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2038.png)

I make sure the destination port ranges is set to 8080 and click Add.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2039.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2040.png)

I go back to the tab using port 8080 and refresh the page and the Jenkins login page has loaded. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2041.png)

I run `cat /var/lib/jenkins/secrets/initialAdminPassword` in the terminal to get the initialPassword, copy and paste it below 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2042.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2043.png)

I click Install suggested plugins and wait until the plugins have been installed.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2044.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2045.png)

Full in detail for the admin user and click Save and Continue. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2046.png)

I click Save and Finish.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2047.png)

Maven & GIT setup in Jenkins Server:

13. In the terminal, I `cd /opt/` and then I run `wget [https://archive.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz](https://archive.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz)`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2048.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2049.png)

I then run `ls-ltra` and see maven download. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2050.png)

After I run `tar -zxvf apache-maven-3.6.0-bin.tar.gz` 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2051.png)

I run `ls-ltra` again and see that at the bottom the download has been unzipped. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2052.png)

Now I can delete the download by running `rm -rf apache-maven-3.6.0-bin.tar.gz`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2053.png)

Now I will go through the process of installing `mvn` , first I run `cd root/` to enter the root directory and edit the bash_profile running `vi .bash_profile` I export Maven and give the path, also added the maven variable to the home /bin/ path. Then I save and quit.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2054.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2055.png)

Then I refresh the file with the source command `source ~/.bash_profile` and after run `mvn`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2056.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2057.png)

Next I install git running `yum install git` 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2058.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2059.png)

Docker setup in Jenkins Server: 

14. First I make sure I’m still connected to the Jenkins Server on the browser and then I head back to my terminal by running `yum install docker` and wait till the installation is done.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2060.png)

15. I run `systemctl start docker` to start the docker software.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2061.png)

16. Then `systemctl enable docker` 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2062.png)

17. I provide permissions to Jenkins user in Jenkins server to access docker using `sudo groupadd docker`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2063.png)

Then I run `sudo usermod -aG docker jenkins` to add the user account. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2064.png)

Afterwards, I provide permission on this file. `sudo chmod 777 /var/run/docker.sock`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2065.png)

18. I run `vi /etc/passwd` and edit the automation server to bash not false.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2066.png)

After that I run `su - jenkins` to login as the Jenkins user. After I run a `id` to see what is install within Jenkins. 

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2067.png)

I `exit` out the Jenkins user and then add Jenkins user into sudoers file to get sudo access by running `vi /etc/sudoers` to open file.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2068.png)

I head all the way down to ‘Allow root to run any commands anywhere’ and under the root command I put `jenkins ALL=(ALL) NOPASSWD: ALL`

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2069.png)

Install and configure Docker & Maven plugin in Jenkins server:

19. I head over to the Jenkins server on my browser and go to manage Jenkins. I search for maven and docker.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2070.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2071.png)

And I tick each plugin and select install without restart and after installation I pick restart Jenkins with no jobs running.

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2072.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2073.png)

![Untitled](Setup%20Jenkins%20in%20AKS%20Cluster%20for%20CI%20CD%2023219459193b4adcb087d9f10b836016/Untitled%2074.png)
