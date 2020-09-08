# Getting Started with App Engine <img src="https://github.com/lordgape/GCP/blob/master/img/app-engine.jpg" />


### Objectives
In this lab, you learn how to perform the following tasks:

- Initialize App Engine.

- Preview an App Engine application running locally in Cloud Shell.

- Deploy an App Engine application, so that others can reach it.

- Disable an App Engine application, when you no longer want it to be visible.

#### Task 1: Initialize App Engine

1. Initialize your App Engine app with your project and choose its region:

        gcloud app create --project=$DEVSHELL_PROJECT_ID
    
    
2. Clone the source code repository for a sample application in the hello_world directory:

        git clone https://github.com/GoogleCloudPlatform/python-docs-samples

3. Navigate to the source directory:

        cd python-docs-samples/appengine/standard_python3/hello_world
    
#### Task 2: Run Hello World application locally

1. Execute the following command to download and update the packages list.

        sudo apt-get update
    
2. Set up a virtual environment in which you will run your application. Python virtual environments are used to isolate package installations from the system.

        sudo apt-get install virtualenv
    
    ``` If prompted [Y/n], press Y and then Enter. ```
 <br/>   
        
        virtualenv -p python3 venv
    
3. Activate the virtual environment.

        source venv/bin/activate
    
4. Navigate to your project directory and install dependencies.

        pip install  -r requirements.txt
    
5. Run the application:

        python main.py
    
    ``` Please ignore the warning if any. ```
   
  #### Task 3: Deploy and run Hello World on App Engine
  
  1. Navigate to the source directory:
  
            cd ~/python-docs-samples/appengine/standard_python3/hello_world
  
  2. Deploy your Hello World application. 
  
            gcloud app deploy
      
      
      ``` If prompted "Do you want to continue (Y/n)?", press Y and then Enter. ```
 <br/>

      This app deploy command uses the app.yaml file to identify project configuration.
      
      
#### Task 4: Disable the application
      
App Engine offers no option to Undeploy an application. After an application is deployed, it remains deployed, although you could instead replace the application with a simple page that says something like "not in service."

However, you can disable the application, which causes it to no longer be accessible to users. 

1. Replace the app.yml content with
    
            module: default \
            runtime: python27 \
            api_version: '1.0' \
            threadsafe: true \
            handlers: \
                - url: / \
                static_files: index.html \
                upload: index.html \
            manual_scaling: \ 
            instances: 1
  
2. Create a dummy ```index.html``` with content
<br>
        
            <title>CLOSED</title>
    
3. Identfy and get app version

            gcloud app versions list
    
    ```Get the app version and replace it for VERSION_ID in the next command```
<br />  
4. Stop version

         gcloud app versions stop VERSION_ID
    
   ``` If you refresh access application site from browser, you'll get a 404 error. ```
   
### Congratulations!
You created your first application using App Engine!

<em>Chesvic Hillary &copy; 2020 </em>
   
  
  

    
