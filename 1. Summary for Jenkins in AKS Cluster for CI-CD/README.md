# Summary for Jenkins in AKS Cluster for CI/CD

This project is focused on build a Continuous Integration and Continuous Delivery/Deployment using Azure Kubernetes Service with Helm. 

I go through setting up Jenkins in a AKS cluster for CI/CD, going over making a Jenkins server Azure DevOps, configuring the virtual machine to host CentOS as the image.
I picked CentOS because it supports 2 cpu’s and 4 GB of ram in which I need in order to run maven later. 

Once I configure the settings for the virtual machine image, I create a SSH key on azure, download the copy of the key, run chmod for permissions and ssh into the Jenkins server virtual machine that was created. 
Afterwards I go through the steps of installing Java-1.8 inside repos directory inside my Jenkins server. 
I also had to update the bash profile.

I needed to use wget to run some commands to download the Jenkins repo, import the key for the Jenkins package (redhat-stable)  for my virtual machine. Once done, I ran the yum install jenkins command.

Next I needed to setup a security group on azure, added an inbound rule on the networking tab and the rule was to make sure the destination port ranges is et to 8080. 

I go back to the tab using port 8080 and refresh the page and the unlock Jenkins page appeared. 
So I ran the command given on the page in the terminal to find the admin password and pasted the password back on the Jenkins tab. 

I choose suggested plugins and waited until the installation was completed. 
Filled in admin user credentials and Jenkins dashboard loaded up. 

For Maven and GIT, I used wget to fetch the maven bin file download, unzipped the download, configured the bash profile, exporting maven and gave the path, added a variable to point maven to bin path. Then updated the bash profile. After that I ran the command to install git using yum. 

The Docker setup in the Jenkins server was me running simple docker commands to get Docker up and running. Providing permissions files for the Jenkins user in the Jenkins server to access Docker. I add the user once done using the sudo usermod… command and then I edited the /etc/passwd file and change the automation server to bash.

Once that was done, I'd used sudo on the jenkins docker container server. Afterwards I headed back to the Jenkins tab on my browser, in manage plugins tab I install Maven integration and Docker pipeline.
