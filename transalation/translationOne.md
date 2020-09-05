# Objectives
In this lab, you will learn how to perform the following tasks:

- Create two Compute Engine virtual machines using the gcloud command-line interface.

- Connect between the two instances.

#### Task 1 : Create two VM Instances

1. You will need google's cloud sdk install on your local machine to run cloud commands from CLI. 
- See <a href="https://cloud.google.com/sdk/docs/downloads-versioned-archives">Download and Install Google cloud sdk</a>  

2. Let's create the first virtual instance called ``` my-vm-1 ``` in ```us-central1-a``` zone and allow http traffic
<br/>



        gcloud config set compute/zone us-central1-a

     <br/>

        gcloud compute instances create "my-vm-1" \ 
        --machine-type "n1-standard-1" \
        --image-project "debian-cloud" \ 
        --image "debian-9-stretch-v20190213" \ 
        --subnet "default" --tags "http" 

    <br/>

            gcloud compute firewall-rules \
            create allow-http --action=ALLOW \ 
            --destination=INGRESS \
            --rules=http:80 --target-tags=http

3. Let's create the second virtual instance called ```my-vm-2``` in ```us-central1-b``` zone.
<br/> 


        gcloud config set compute/zone us-central1-b
    <br/>

        gcloud compute instances create "my-vm-2" \ 
        --machine-type "n1-standard-1" \
        --image-project "debian-cloud" \ 
        --image "debian-9-stretch-v20190213" \ 
        --subnet "default"


#### Task 2: Connect between the VM Instances

1. Let's confirm that virtual machine ```my-vm-2``` can reach ```my-vm-1``` over the network.

-   Tunnel into virtual machine ```my-vm-2``` using ssh from CLI.

        gcloud compute ssh my-vm-2

- Check if virtual machine ```my-vm-1``` is reachable 

        ping -c 4 my-vm-1

    
- <b>Please Note</b> 
       
         Notice that the output of the ping command reveals that the complete hostname of my-vm-1
         is my-vm-1.c.PROJECT_ID.internal, where PROJECT_ID is the name of your Google Cloud 
         Platform project. GCP automatically supplies Domain Name Service (DNS) uresolution 
         for the internal IP addresses of VM instances.

     Since our ping was successful. It means we can reach virtual machine ```my-vm-1``` from ```my-vm-2```

 2. Now, let's host a static web page on virtual machine ```my-vm-1``` and see if we can access the page from virtual machine ```my-vm-2```

- Use the ssh command to open a command prompt on virtual machine ```my-vm-1```

        ssh my-vm-2

     If you are prompted about whether you want to continue connecting to a host with unknown authenticity, enter <b>yes</b> to confirm that you do. 
<br/>

- At the command prompt on ``` my-vm-1 ```, install the Nginx web server:

        sudo apt-get install nginx-light -y

- Use the nano text editor to add a custom message to the home page of the web server:

        sudo nano /var/www/html/index.nginx-debian.html

     Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace ```YOUR_NAME``` with your name:
<br/>

        Hi from YOUR_NAME

     Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.
<br/>

- Confirm that the web server is serving your new page. At the command prompt on ```my-vm-1```  , execute this command:
    
        curl http://localhost/

    The response will be the HTML source of the web server's home page, including your line of custom text.
<br/>

- To exit the command prompt on ```my-vm-1```, execute this command:

        exit

- To confirm that ```my-vm-2``` can reach the web server on ```my-vm-1```, at the command prompt on ```my-vm-2```, execute this command:

        curl http://my-vm-1/

    The response will again be the HTML source of the web server's home page, including your line of custom text.