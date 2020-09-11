# GCP-Practice-Project
A repo to display my GCP Practice Project

# TRANSLATION CODE

# Lab 1: Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives:
In this lab, you will learn how to perform the following tasks:

Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

Create a Compute Engine virtual machine using the gcloud command-line interface.

Connect between the two instances.

Step A:
  1.  to Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console. since this project involves translation into command line,
 
 <!--  i use the command below to create a virtual machine using the command google command line the following code created a virtual machine name my-vm-1 -->
  gcloud compute instances create "my-vm-1"--machine-type "n1-standard-1"--image-project "debian-cloud--image "debian-9-stretch-v20190213"--subnet "default" --tags http

 <!--  this command sets the region and zone of the instance created.-->
  gcloud config set compute/zone us-central1-b

 2. then i created a fire wall rule to enable the virtual machine to be accessible by other virtuaL machines 
  <!-- these command when typed in the google cloud command line lets you alliow inbound traffic to your instance -->
 gcloud compute firewall-rules create allow-http--action=ALLOW--destination=INGRESS--rules=http:80--target-tags=http

 3.  then i Created  another Compute Engine virtual machine named my-vm-2  and set the region and zone also using the gcloud command-line interface above.

gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213"--subnet "default"

gcloud config set compute/zone us-central1-b


Step B:Connect between the two instances.

  <!-- Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network: -->
in other to reach the other virtual machine created from the command line connect to one of the virtual machines using the ssh command and test the network connectivity using the ping commmand

Connect to my-vm-2:
 <!--this command lets you connect to a the virtual machine instance/-->
  gcloud compute ssh my-vm-2

<!-- this code lets you test the connectivity from one vm to the other/-->
  Ping my-vm-1 from my-vm-2:
  ping -c 4 my-vm-1

Use the ssh command to open a command prompt on my-vm-1 from my-vm-2:

ssh my-vm-1

At the command prompt on my-vm-1, install Nginx web server:

sudo apt-get install nginx-light -y

Use the nano text editor to add a custom message to the home page of the web server:

sudo nano /var/www/html/index.nginx-debian.html

Add text like this, and replace YOUR_NAME with your name:

Hi from Domo

Exit the editor and confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:

curl http://localhost/

Result: The response will be the HTML source of the web server's home page, including your line of custom text.

To exit the command prompt on my-vm-1, execute this command:

exit

To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

curl http://my-vm-1/

Result: The response will again be the HTML source of the web server's home page, including your line of custom text.

Now get the external IP of the my-vm-1 instance from this command:

gcloud compute instances list --zone us-central1-a

Paste the copied IP address of my-vm-1 into a new browser tab and hit enter:

Result: You will see your web server's home page, including your custom text.
