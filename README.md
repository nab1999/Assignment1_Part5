# Assignment1_Part5

## Part 5: Multi-Container Application Deployment using Docker Compose

### Step1: (Create a Dockerfile for the web application container which should include the necessary dependencies to run the web application. The web application should display a simple "Hello, World!" message when accessed from a web browser)

#### Section 1.1.0

Installing Flask in “assignment1_part5” directory. This directory will contain all the files for this part 5 of the assignment.

![image](https://user-images.githubusercontent.com/126570628/227796021-6610329c-217e-44c1-96c1-a90b34517cf2.png)

#### Section 1.1.1

In this section, we will create a Python file “web.py” that receives and respond to requests in our application.

![image](https://user-images.githubusercontent.com/126570628/227796069-bd18b315-2090-41ec-8547-563faaf63d25.png)

#### Section 1.1.2

In this section, we will create a HTML file “index.html” that will provide content we want to render on browser when we invoke the home() function in the “web.py” file.

![image](https://user-images.githubusercontent.com/126570628/227796090-51e7c2cf-11c5-48dc-ac40-bbec7c270207.png)

#### Section 1.1.3

In this section, we will create a “requirements.txt” file which contains the list of packages and dependencies that we need to run our project and their respective versions.

![image](https://user-images.githubusercontent.com/126570628/227796109-304f29d4-ff9a-4c33-a919-d88c1c370bfe.png)

#### Section 1.1.4

Testing the “web.py” file or application on our local machine.

![image](https://user-images.githubusercontent.com/126570628/227796125-973a8f91-7cc6-4f06-8065-864cd431c10b.png)

![image](https://user-images.githubusercontent.com/126570628/227796137-3e28669b-165b-4231-bc67-75773df9c26b.png)

#### Section 1.1.5

Making a docker file for the web application.

![image](https://user-images.githubusercontent.com/126570628/227796157-4ad8ba9f-4171-40b9-bfa8-ced63085fc98.png)

#### Section 1.1.6

Moving all files related to web application to a new directory called “web_app” in order to easily distinguish or simply things.

![image](https://user-images.githubusercontent.com/126570628/227796177-d6b2cdb4-e215-4960-a66e-baba54659b0d.png)

#### Section 1.1.7

Building a docker image file “web_image” for the web application.

![image](https://user-images.githubusercontent.com/126570628/227796246-4a58824e-9ee1-4158-8d79-76247ca9cdd9.png)

### Step2: (Create a Dockerfile for the database “PostgreSQL” container which should include the necessary dependencies to run the database)

#### Section 2.1.0

Creating a Dockerfile for database “PostgreSQL”.

![image](https://user-images.githubusercontent.com/126570628/227796281-a4f0f1df-f533-48de-a901-ec208bed57c4.png)

1. (FROM postgres): This tells docker to pull “postgres” image.

2. (ENV POSTGRES_PASSWORD postgres) & (ENV POSTGRES_DB testdb): We set up values of two environment (ENV) variables POSTGRES_PASSWORD and POSTGRES_DB to be postgres and testdb respectively.

3. (COPY init.sql /docker-entrypoint-initdb.d/): Finally input (COPY) an init.sql file, located in the same folder as Dockerfile, to the /docker-entrypoint-initdb.d/ folder located in postgres Docker image that we’re using. By default, all scripts located in this folder will be automatically ran during container startup.

#### Section 2.1.1

Creating a “init.sql” file and putting all the SQL scripts. In our case it’s a single script to create a table.

![image](https://user-images.githubusercontent.com/126570628/227796329-b58cf76d-832f-4ba5-810d-8e50c0e7a343.png)

#### Section 2.1.2

Building a docker image file “db_image” for the database.

![image](https://user-images.githubusercontent.com/126570628/227796343-0ce1004f-a698-4570-be30-11f8f5063f2c.png)

### Step3: (Create a docker-compose.yml file that defines the two services - web and database)

![image](https://user-images.githubusercontent.com/126570628/227796360-65cbd6e8-3b52-4dff-86ff-55779e1c74b3.png)

### Step4: (Use the docker-compose up command to build and run the application.)

#### Section 4.1.0

Executing “docker-compose up” command:

![image](https://user-images.githubusercontent.com/126570628/227796379-a0b52bbb-80d1-4435-b481-46e0cbbf02e5.png)

Dockers(web_app_container & db_postgres_container)created and running:

![image](https://user-images.githubusercontent.com/126570628/227796390-1c2f068d-4a29-4caa-bf28-be47780fd6d6.png)

#### Section 4.1.1

Web application running and can be accessed on the local machine CLI when we send a request to localhost:5000.

![image](https://user-images.githubusercontent.com/126570628/227796415-eba8e2e7-4c0d-440c-b2b9-e3082182091b.png)

Accessing the running database container “db_postgress_container” and then working with the PostgreSQL database “testdb” and checking the table “persons” which was determined in the dockerfile of the database previously. 

![image](https://user-images.githubusercontent.com/126570628/227796429-3c649b52-6e6f-4dc8-bc7c-618fb804b070.png)

### Step6: (Modify the Dockerfile for the web application container to include a new feature. Rebuild the web application container and redeploy the application using docker-compose)

#### Section 6.1.0

Modifying the background color of the web page in the HTML file:

![image](https://user-images.githubusercontent.com/126570628/227796451-5809283f-f271-46a5-8174-0de42e6e28b8.png)

#### Section 6.1.1

Building a new image based on Dockerfile:

![image](https://user-images.githubusercontent.com/126570628/227796471-71579b29-380b-48a2-9ab8-a5b40c647d0f.png)

![image](https://user-images.githubusercontent.com/126570628/227796476-d123c451-6163-417e-8f0a-131aed1f229c.png)

#### Section 6.1.2

Rebuilding and redeploying containers using “docker-compose up -d” command based on “docker-compose.yml” YAML file.

![image](https://user-images.githubusercontent.com/126570628/227796496-33dc233e-6613-4bdd-b573-a5265a3af963.png)

#### Section 6.1.3

Verifying new feature (background color to blue) working as expected:

![image](https://user-images.githubusercontent.com/126570628/227796516-1d0aac7c-dca0-40d4-b555-40721a791514.png)

### Step7: (Implement a backup strategy for the database)

Implementing a backup strategy for the database using Docker volume. The database volume is linked or has a backup in the local machine volume with the path : “./data/db” as shown below.

![image](https://user-images.githubusercontent.com/126570628/227796524-ca3c3db5-08ca-4598-8420-bfbcef4d03c7.png)

### Step8: (Implement a scaling strategy for the web application)

#### Section 8.1.0

Changing ports for “web-app” service to “– 5000” which will the port 5000 of the container to an ephemeral unallocated port on the host machine. The problem with our current configuration was that we’re trying to run three instances of the web-app service and map them all to the same port on our host machine. Because the host machine can only bind an unallocated port to the container, we will get the “Bind for 0.0.0.0:5000 failed: port is already allocated” error for each additional web-app service, hence we will not be able to scale our web application.

![image](https://user-images.githubusercontent.com/126570628/227796547-062337a9-557a-45f1-94e5-efd46254a78f.png)

#### Section 8.1.1

Executing “docker-compose up -d –scale web-app=3” command to scale our web application to three instances as shown below.

![image](https://user-images.githubusercontent.com/126570628/227796558-df9209b1-0d43-4b76-97c0-4c7875e274dd.png)

#### Section 8.1.2

By running the command “docker-compose ps” we can see that  web-app containers are running at ports 49154, 49155, and 49153. And all three of them are accessible as shown below.

![image](https://user-images.githubusercontent.com/126570628/227796583-e0ba833b-e7b5-49ff-9ce7-4b74ef34302c.png)

### Step9: (Implement a monitoring strategy for the application)

Implementing Grafana to monitor the health and performance of the containers.

#### Section 9.1.0

Dockerfile configurations:

![image](https://user-images.githubusercontent.com/126570628/227796600-c2e40d82-016a-4bfd-8f6e-598216c1f07c.png)

#### Section 9.1.1

Building and running docker containers by using “docker-compose up -d” command:

![image](https://user-images.githubusercontent.com/126570628/227796616-ffd6129c-c5d0-464a-b4b9-b516039a50d8.png)

![image](https://user-images.githubusercontent.com/126570628/227796620-b69754e0-b4e3-4c41-adeb-2e5e11f3bc6d.png)

#### Section 9.1.2

Accessing Grafana through “localhost:3000”.

![image](https://user-images.githubusercontent.com/126570628/227796629-741eca70-be72-4518-bf75-94fa342902a5.png)

### Step10: (Create a README.md file)

Created a README.md file in “Assignment1_Part5” GitHub repository under the main branch. This file contains the findings for each command used in Part 5 of the assignment.

### Step11: (Push the codebase for the sample application to your GitHub repository)

Initializing git in “assignment1_part5” directory, and then committing the sample application files to local repository.

![image](https://user-images.githubusercontent.com/126570628/227796670-b4520392-150b-481c-9195-52499f000a96.png)

Then we pushed the codebase for the sample flask application to the GitHub repository under master branch by first setting the remote repository configuration: “git remote add origin  https://github.com/nab1999/Assignment1_Part5.git” and then pushing the local git repository to remote/central/GitHub repository by using the command: “git push -u origin master”. To verify that is has been pushed successfully we can check the files in the GitHub repository in the browser. And to pull the files/repository to our local machine/repository, we can use the command “git pull -u origin master”.

![image](https://user-images.githubusercontent.com/126570628/227796684-123e6026-42f2-4c87-bdfb-48931f8fdd3d.png)

![image](https://user-images.githubusercontent.com/126570628/227796690-ed70635a-2c7f-4880-bb44-0c19d3a18e31.png)

