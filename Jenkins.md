
1. **Spin up an EC2 server** and expose the following ports in the security groups for the EC2 instance:
    1. `80` for HTTP
    2. `443` for HTTPS
    3. `4040` for the Docker container running on the EC2 instance to receive incoming traffic
    4. `8080` for Jenkins (Jenkins comes with its own web server called Jetty, so you don’t need to serve it through a web server like Nginx)

2. **SSH into the EC2 server**.

3. **Install Docker and Jenkins**:
    - The exact steps to install Docker and Jenkins depend on the OS your EC2 instance is running.
    - After installing Jenkins, you will need to retrieve the initial admin password for Jenkins, which will be required when logging in for the first time. You can get this password by running the following command on your EC2 instance:
