# 🚀 Deploying a Dockerized Application on AWS EC2

This guide outlines the steps to deploy a Dockerized application on an AWS EC2 instance using Docker and DockerHub.

---

## 📦 1. Build Docker Image (Locally)

```bash
docker build -t your-image-name .
☁️ 2. Push Image to DockerHub
docker login
docker tag your-image-name your-dockerhub-username/your-image-name
docker push your-dockerhub-username/your-image-name
💻 3. Launch an AWS EC2 Instance
Go to AWS EC2 Console

Launch a new instance:

Choose Amazon Linux 2 or Ubuntu

Select instance type (e.g., t2.micro for free tier)

Create or use an existing key pair (save .pem file)

Configure security group to allow:

SSH (port 22)

App port (e.g., 80, 3000, etc.)

Launch and wait for instance to initialize.

🔐 4. Connect to Your EC2 Instance
bash
Copy
Edit
ssh -i /path/to/your-key.pem ec2-user@your-ec2-public-ip
For Ubuntu, replace ec2-user with ubuntu

🐳 5. Install Docker on EC2
For Amazon Linux 2:
bash
Copy
Edit
sudo yum update -y
sudo yum install docker -y
sudo service docker start
sudo usermod -aG docker ec2-user
Log out and back in for the group changes to take effect.

For Ubuntu:
bash
Copy
Edit
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo usermod -aG docker $USER
Log out and back in for the group changes to take effect.

📥 6. Pull Docker Image from DockerHub
bash
Copy
Edit
docker pull your-dockerhub-username/your-image-name
▶️ 7. Run the Docker Container
bash
Copy
Edit
docker run -d -p 80:3000 your-dockerhub-username/your-image-name
This maps container port 3000 to host port 80. Modify ports as needed.

🌐 8. Access Your Application
In your browser, go to:

cpp
Copy
Edit
http://<your-ec2-public-ip>
Ensure the port is open in the EC2 security group.

✅ Done!
Your Dockerized application is now live on AWS EC2. 🎉

