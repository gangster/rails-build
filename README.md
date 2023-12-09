# Overview
This project provides a Dockerized environment for building and deploying a Ruby on Rails application. It is designed to support both local development and production deployment seamlessly. Additionally, it offers support for multiple system architectures, such as amd64 and arm, allowing flexibility in deployment targets.

# Prerequisites
Before you begin, make sure you have the following prerequisites installed on your system:

**Docker**: Ensure you have Docker installed on your local machine for containerization.

## Usage

### Local Development

To run the Ruby on Rails application for local development, follow these steps:

1. **Fork this repository**: Click the "Fork" button at the top right of this repository's page to create a copy of it in your GitHub account.

2. **Clone your fork**: After forking, clone your forked repository to your local machine:
  ```bash
  git clone https://github.com/yourusername/your-project.git
  cd your-project
  ```
3. **Build the development container**:
  ```bash
  docker-compose build
  ```

4. **Start the development server**:
  ```bash
  docker-compose up
  ```
  This will start the Rails application and PostgreSQL database in separate containers. You can access the application at http://localhost:8000 in your web browser.


5. You can make code changes locally, and the changes will be reflected in the running application without the need for extra setup.  

### Production Deployment

For deploying the container in a production environment, this project utilizes GitHub Actions to automate the build and publish steps by pushing a [multi-architecture image](https://github.com/gangster/rails-build/pkgs/container/rails-build) to the [Github package registry](https://github.com/gangster/rails-build/pkgs/container/rails-build), making it easily accessible for deployment in various scenarios. This image can be referenced in deployment files, such as Docker Compose or Kubernetes manifests.

This image may also be pulled locally for closer inspection:
```bash
docker pull ghcr.io/gangster/rails-build:main
```

And if we do inspect it, we notice that everything the app needs to run in prod is minted inside the container.
```bash
❯ docker run -it ghcr.io/gangster/rails-build:main ls -al
total 112
drwxr-xr-x  1 root  root  4096 Dec  9 20:31 .
drwxr-xr-x  1 root  root  4096 Dec  9 21:44 ..
-rw-r--r--  1 root  root   703 Dec  9 20:30 .dockerignore
-rw-r--r--  1 root  root   348 Dec  9 20:30 .gitattributes
drwxr-xr-x  3 root  root  4096 Dec  9 20:30 .github
-rw-r--r--  1 root  root   815 Dec  9 20:30 .gitignore
-rw-r--r--  1 root  root    11 Dec  9 20:30 .ruby-version
-rw-r--r--  1 root  root  1885 Dec  9 20:30 Dockerfile
-rw-r--r--  1 root  root  2118 Dec  9 20:30 Gemfile
-rw-r--r--  1 root  root  6026 Dec  9 20:30 Gemfile.lock
-rw-r--r--  1 root  root   374 Dec  9 20:30 README.md
-rw-r--r--  1 root  root   227 Dec  9 20:30 Rakefile
drwxr-xr-x 10 root  root  4096 Dec  9 20:30 app
drwxr-xr-x  2 root  root  4096 Dec  9 20:30 bin
-rw-r--r--  1 root  root   595 Dec  9 20:30 compose.yml
drwxr-xr-x  5 root  root  4096 Dec  9 20:30 config
-rw-r--r--  1 root  root   160 Dec  9 20:30 config.ru
drwxr-xr-x  1 rails rails 4096 Dec  9 20:30 db
drwxr-xr-x  4 root  root  4096 Dec  9 20:30 lib
drwxr-xr-x  1 rails rails 4096 Dec  9 20:30 log
drwxr-xr-x  3 root  root  4096 Dec  9 20:42 public
drwxr-xr-x  1 rails rails 4096 Dec  9 20:30 storage
drwxr-xr-x 10 root  root  4096 Dec  9 20:30 test
drwxr-xr-x  1 rails rails 4096 Dec  9 20:42 tmp
drwxr-xr-x  2 root  root  4096 Dec  9 20:30 vendor
```


