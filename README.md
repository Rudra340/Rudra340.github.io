# Rudra340.github.io
Tutorial for Docker Hub Images

#**Title: Building a Three-Tier Application with Docker: A Step-by-Step Guide**

Welcome to our comprehensive tutorial on building a three-tier application using Docker! In this guide, we'll walk you through every step, from setting up your environment to deploying a multi-container application. Let's dive in!

Part 1: Introduction and Setup

Hello fellow Docker enthusiasts! Today, we're embarking on an exciting journey to build a three-tier application using Docker. In this tutorial, we'll walk through each step, from setting up our environment to deploying our multi-container application.

Step 1: Setting Up

First things first, let's ensure we have Docker installed on our system. If you haven't already installed Docker, head over to the official Docker website and follow the installation instructions for your operating system.

Once Docker is installed, verify that it's running by opening your terminal (or command prompt) and typing:

bash
Copy code
docker --version
You should see the Docker version displayed, indicating that Docker is installed and running correctly.

Step 2: Project Selection

For this tutorial, we'll be building a simple three-tier application consisting of a front-end, a back-end, and a database. You're free to use your own project or choose one from GitHub. If you opt for a project from GitHub, be sure to properly cite the original author in your blog post.

Step 3: Clone the Repository

If you're using a project from GitHub, clone the repository to your local machine using the following command:

bash
Copy code
git clone <repository-url>
Replace <repository-url> with the URL of the GitHub repository you've chosen.

Step 4: Project Structure

Now that we have our project ready, let's take a quick look at its structure. Navigate to the project directory and explore its contents. You should see files related to the front-end, back-end, and any other components of the application.

In our example, we have a frontend, backend, and database directory, each containing the respective code for our application's components.

Step 5: Dockerfile Creation for Front-End

Next, let's create Dockerfiles for each component of our application. We'll start with the front-end. Create a file named Dockerfile (without any file extension) inside the frontend directory. Open the Dockerfile in your favorite text editor and add the following content:

Dockerfile
Copy code
# Use an official Node.js runtime as the base image
FROM node:14

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose port 3000 to the outside world
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]
Let's break down what each line in the Dockerfile does:

FROM node:14: Specifies the base image for our front-end container, which is a Node.js runtime.
WORKDIR /app: Sets the working directory inside the container to /app.
COPY package*.json ./: Copies the package.json and package-lock.json files from our host machine to the working directory in the container.
RUN npm install: Installs dependencies specified in package.json.
COPY . .: Copies the rest of the application code from our host machine to the working directory in the container.
EXPOSE 3000: Exposes port 3000, which is the default port for our front-end application.
CMD ["npm", "start"]: Specifies the command to run our front-end application when the container starts.
That's it for the Dockerfile of our front-end component! Next, we'll create Dockerfiles for the back-end and database components.

Step 6: Dockerfile Creation for Back-End

Similar to the front-end, we'll create a Dockerfile for the back-end component. Navigate to the backend directory and create a file named Dockerfile. Open the Dockerfile and add the following content:

Dockerfile
Copy code
# Use an official Node.js runtime as the base image
FROM node:14

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose port 5000 to the outside world
EXPOSE 5000

# Command to run the application
CMD ["npm", "start"]
This Dockerfile is similar to the one for the front-end, with minor adjustments for the back-end component.

Step 7: Dockerfile Creation for the Database

For the database component, we'll use an official MySQL image from Docker Hub. Create a directory named database and within it, create a file named Dockerfile. Open the Dockerfile and add the following content:

Dockerfile
Copy code
# Use the official MySQL image as the base image
FROM mysql:8

# Set the root password
ENV MYSQL_ROOT_PASSWORD=root

# Create a database
ENV MYSQL_DATABASE=my_database

# Expose port 3306 to the outside world
EXPOSE 3306
This Dockerfile sets up a MySQL database container with a root password and creates a database named my_database.

Step 8: Docker Compose

Now that we have Dockerfiles for all our components, let's orchestrate the multi-container setup using Docker Compose. Create a file named docker-compose.yml in the root directory of your project and add the following content:

yaml
Copy code
version: '3'

services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"

  backend:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - database

  database:
    build: ./database
    ports:
      - "3306:3306"
This docker-compose.yml file defines three services: frontend, backend, and database, each corresponding to a component of our three-tier application. It specifies the Dockerfiles for building each service and exposes the necessary ports.

Step 9: Running the Application

To run our application, navigate to the root directory of your project in the terminal and run the following command:

bash
Copy code
docker-compose up
Docker Compose will build the necessary Docker images and start the containers for each component. You should see logs indicating that each service is up and running.


**Conclusion**

In this tutorial, we've learned how to build a three-tier application using Docker. We've created Dockerfiles for each component, orchestrated the multi-container setup using Docker Compose, and deployed our application.

We hope you found this tutorial helpful and that you're now ready to embark on your Docker journey. Happy coding!

Thank you for reading.

End of Blog.
