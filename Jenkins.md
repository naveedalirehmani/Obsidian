
1. **Spin up an EC2 server** and expose the following ports in the security groups for the EC2 instance:
    1. `80` for HTTP
    2. `443` for HTTPS
    3. `4040` for the Docker container running on the EC2 instance to receive incoming traffic
    4. `8080` for Jenkins (Jenkins comes with its own web server called Jetty, so you don’t need to serve it through a web server like Nginx)

2. **SSH into the EC2 server**.

3. **Install Docker and Jenkins**:
    - The exact steps to install Docker and Jenkins depend on the OS your EC2 instance is running.
    - After installing Jenkins, you will need to retrieve the initial admin password for Jenkins, which will be required when logging in for the first time. You can get this password by running the following command on your EC2 instance:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

- Once you log in, Jenkins will prompt you to set up a user account, which you will use for subsequent logins.

4. **Dockerize your local `index.html` file** by defining a `Dockerfile` and a `docker-compose.yml` file:
    - In your `docker-compose.yml`, use `nginx:alpine` as the base image, which includes an Nginx server that will serve the `index.html` file from `/usr/share/nginx/html/index.html` on port `80`.

5. **Login to the Jenkins dashboard**, which will be accessible at `http://your-domain-publicip:8080`.

6. **Set up the Jenkins pipeline**:
    1. Install the **GitHub Integration Plugin** to allow Jenkins to communicate with GitHub repositories.
    2. Create a new pipeline in Jenkins:
        1. In the **Pipeline** configuration, scroll down to the **Pipeline** section.
        2. Select **Pipeline script from SCM**.
        3. Choose **Git** as the SCM option.
        4. Enter your **GitHub repository URL** (ensure this is the HTTPS URL, not the SSH URL).

7. **Define a Jenkinsfile** in your code and push it to GitHub. This file will be automatically picked up by Jenkins when you manually trigger the pipeline.

8. **Example Jenkins pipeline configuration**:
    ```groovy
    pipeline {
        agent any

        stages {
            stage('Clone Repository') {
                steps {
                    git branch: 'main', url: 'https://github.com/<your-username>/<your-repo>.git'
                }
            }
            stage('Build Docker Image') {
                steps {
                    script {
                        // Build Docker image
                        sh 'docker-compose up --build -d'
                    }
                }
            }
            stage('Deploy to Nginx on EC2') {
                steps {
                    script {
                        // Run the container on EC2
                        sh 'docker-compose down'
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }
    ```

9. Once everything is set up, go to the Jenkins dashboard and trigger the pipeline manually by clicking **"Build Now"** in the pipeline sidebar.

### Troubleshooting:

- When running the pipeline, you may encounter the following issue:
    1. The Jenkinsfile steps will be executed on the EC2 instance by a user called `jenkins`, which is created by default during the Jenkins installation. This user might not have permission to run commands like `docker-compose up --build`. To resolve this, grant the necessary permissions by editing the sudoers file:

```
sudo visudo
```
    
Add the following line at the bottom of the file:

```
jenkins ALL=(ALL) NOPASSWD: /usr/bin/docker, /usr/bin/docker-compose
```
