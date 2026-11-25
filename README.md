
# Company Landing Page

## Project Overview

This project is a responsive Company Landing Page developed using HTML and CSS. The website is containerized using Docker and deployed automatically using Jenkins CI/CD pipeline.

## Technologies Used

- HTML5
- CSS3
- Docker
- Nginx
- Jenkins
- GitHub
- Docker Hub
- AWS EC2
- Ubuntu Linux

## Project Features

- Professional company landing page
- Responsive website design
- Modern user interface
- Custom HTML and CSS styling
- Docker containerization
- Automated CI/CD deployment using Jenkins

## Project Structure

```text
open-website/
│
├── Dockerfile
├── Jenkinsfile
├── index.html
├── style.css
└── README.md
```

## Docker Configuration

The application uses the official Nginx Alpine image.

### Build Docker Image

```bash
docker build -t companywebsite:latest .
```

### Run Docker Container

```bash
docker run -d \
  --name company-website \
  -p 9090:80 \
  companywebsite:latest
```

### Verify Container

```bash
docker ps
```

## Jenkins CI/CD Pipeline

The Jenkins pipeline automates the following stages:

1. Checkout source code from GitHub.
2. Build Docker image on the build server.
3. Verify Docker image.
4. Login to Docker Hub.
5. Push Docker image to Docker Hub.
6. Pull the latest image on the deployment server.
7. Stop and remove the old container.
8. Deploy the new Docker container.
9. Verify website deployment.

## Docker Hub Repository

Repository: https://hub.docker.com/r/lubina123/companywebsite

## GitHub Repository

Source Code: https://github.com/lubinafebin7/open-website

## Website Access

After successful deployment, access the website using:

```text
http://YOUR-DEPLOYMENT-PUBLIC-IP:9090
```

## Deployment Architecture

- Jenkins Server: Pipeline management.
- Build Server: Docker image build and push.
- Deployment Server: Docker image pull and container deployment.

## Conclusion

This project demonstrates how to develop, containerize, and deploy a company landing page using modern DevOps tools and an automated Jenkins CI/CD pipeline.
