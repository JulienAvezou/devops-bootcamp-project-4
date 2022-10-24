# devops-bootcamp-project-4
Demo for Module 8: CI/CD and Jenkins

1. Create server on DigitalOcean and config firewall rule for Jenkins. Install Docker

2. Pull and run Jenkins container -> docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

3. Install build tools in Jenkins container (using Jenkins plugin manager and/or installing directly on server on which Jenkins container is running)

4. Create a simple job in Jenkins and run a build
<img width="1070" alt="1" src="https://user-images.githubusercontent.com/62488871/197352080-4d0e2f62-641b-4dc7-a097-d9bfab96a9fa.png">

5. Configure Jenkins access to Source Code Mgmnt (Github in this case)
<img width="1000" alt="2" src="https://user-images.githubusercontent.com/62488871/197352102-89dfd804-c4d6-4c4b-946c-81620859f186.png">

6. Run another build for the same job and verify that repo was checked out
<img width="839" alt="3" src="https://user-images.githubusercontent.com/62488871/197352132-bfdbdb25-9808-450b-82f0-5f4d530e58b7.png">
<img width="364" alt="4" src="https://user-images.githubusercontent.com/62488871/197352139-9cfafc3c-7278-4b21-8ddf-06c65c9a9c48.png">

7. Add 'package' command from maven to build steps, when checking out branch on github repo, and verify that artifact was built successfully
<img width="1031" alt="5" src="https://user-images.githubusercontent.com/62488871/197352160-ea0be4c3-e966-4a33-952d-4a076e5ceadc.png">

8. Access Docker from Jenkins container -> need to mount Docker runtime directory from host server into the container as a volume
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker --name jenkins jenkins/jenkins:lts

9. Give jenkins user permissions to read and write Docker /var/run/docker.sock
as root user run: chmod 666 /var/run/docker.sock

10. Build Docker image from Jenkins using Dockerfile
<img width="807" alt="6" src="https://user-images.githubusercontent.com/62488871/197352196-284cfe5b-7a0a-49fd-8c72-921199bbfb16.png">
<img width="439" alt="7" src="https://user-images.githubusercontent.com/62488871/197352205-51fbde9e-eae7-4b73-a5f9-382cbbcc45c8.png">

11. Create repo on Dockerhub and add credentials to Jenkins
<img width="849" alt="8" src="https://user-images.githubusercontent.com/62488871/197352215-e65d4781-ea46-45b1-9c17-fe6e82f42e4c.png">

12. Add Docker scripts in Jenkins job build to login to Dockerhub using credentials added and push to the Dockerhub repo (for credentials use secret texts to create variables used in commands for login)
<img width="979" alt="9" src="https://user-images.githubusercontent.com/62488871/197352270-4d0a7213-8b58-4e22-b307-0536321807a3.png">
<img width="561" alt="10" src="https://user-images.githubusercontent.com/62488871/197352287-c928533e-9395-4614-af70-9663fc0b3ac5.png">

13. Run the build and check in Dockerhub repo that image is there
<img width="804" alt="11" src="https://user-images.githubusercontent.com/62488871/197352303-8747ec1c-e2fb-4433-aceb-aac812ed5351.png">
<img width="725" alt="12" src="https://user-images.githubusercontent.com/62488871/197352307-39db1ee9-8a6e-4f33-a4d8-b640f4046dff.png">

14. Create pipeline job that connects to Git repo
<img width="1056" alt="13" src="https://user-images.githubusercontent.com/62488871/197352317-d494e0a7-b104-476f-a390-f251191fc52d.png">

15. Create Jenkinsfile in configured repo
<img width="404" alt="14" src="https://user-images.githubusercontent.com/62488871/197352320-6fa09901-b960-4f91-a7c8-2bd84edfb277.png">

16. Build pipeline job
<img width="1175" alt="15" src="https://user-images.githubusercontent.com/62488871/197352323-cedd50f5-dfe5-4765-ba0f-b8b54546a201.png">

17. Enhance pipeline job to build jar and push to Docker hub
<img width="1229" alt="16" src="https://user-images.githubusercontent.com/62488871/197352334-b97545b2-5ebd-4348-956f-1e1b968ab95e.png">
<img width="1069" alt="17" src="https://user-images.githubusercontent.com/62488871/197352337-af1aa231-48a0-4c0d-8aba-63b5b7cea114.png">

18. Create multibranch pipeline
<img width="534" alt="18" src="https://user-images.githubusercontent.com/62488871/197352348-facee911-f3d9-40b2-888f-c4fe5a2abcf0.png">
<img width="1059" alt="19" src="https://user-images.githubusercontent.com/62488871/197352349-2969b575-cfdd-41b1-8280-a93270146454.png">

19. Create Jenkins Shared Library
<img width="927" alt="20" src="https://user-images.githubusercontent.com/62488871/197352356-442315ad-b499-4ab6-9511-91113c06964c.png">

20. Configure Jenkins to be able to use Shared Library
<img width="978" alt="21" src="https://user-images.githubusercontent.com/62488871/197352361-64f0ad22-c09b-4027-96ff-b139ffcf94a4.png">

21. Use Shared Library in Jenkinsfile
<img width="508" alt="22" src="https://user-images.githubusercontent.com/62488871/197352375-b4434b64-bcb2-45a0-920e-accfb64a76ef.png">

22. Refactor Jenkins Shared Library & Jenkinsfile to use groovy classes and separate functions, and scope to project
<img width="1260" alt="23" src="https://user-images.githubusercontent.com/62488871/197352400-9dfe998e-6d4a-4006-a712-76515974c0d7.png">
<img width="522" alt="24" src="https://user-images.githubusercontent.com/62488871/197352402-c0142a66-a8d0-415a-ad43-617a53fa59c7.png">
<img width="625" alt="25" src="https://user-images.githubusercontent.com/62488871/197352406-b1d76cce-e74e-4a21-a693-d286cfb07e9f.png">
<img width="731" alt="26" src="https://user-images.githubusercontent.com/62488871/197352409-c59e6d4a-266f-46ce-bf1a-9a94d07a6ca0.png">

23. Configure webhook to trigger pipeline jobs automatically 
<img width="997" alt="Capture d’écran 2022-10-23 à 21 31 53" src="https://user-images.githubusercontent.com/62488871/197414488-d4a0bb86-fc6f-4df2-8b5b-15acca002fcd.png">
<img width="797" alt="Capture d’écran 2022-10-23 à 21 35 18" src="https://user-images.githubusercontent.com/62488871/197414493-eb778850-cbd7-4bb9-b6ec-6517d6ea1b4f.png">

24. Automatically increment app version using Jenkins pipeline
- parse and increment app version, store result in variable and use it to increment the Docker image tag
<img width="1128" alt="Capture d’écran 2022-10-24 à 20 55 09" src="https://user-images.githubusercontent.com/62488871/197604898-ce0b877d-76e6-45ac-a328-a0682485af3b.png">
<img width="488" alt="Capture d’écran 2022-10-24 à 21 00 38" src="https://user-images.githubusercontent.com/62488871/197604929-23151735-92a8-4412-b3e7-a0a4232d6a4f.png">

- modify Dockerfile so that it builds from any jar file
- clean packages so that Dockerfile builds image from the correct jar file
