# 🌐 Module 5 Demo Project: Deploy Java Gradle App on DigitalOcean Droplet

## 🛠️ Technologies Used
- **DigitalOcean** – Cloud infrastructure provider used to host the application.
- **Linux (Ubuntu)** – Server OS on the Droplet.
- **Java** – Application runtime.
- **Gradle** – Build automation tool for managing dependencies and running the app.

---

## 📄 Project Description

This project demonstrates how to manually set up a Linux server on DigitalOcean and deploy a Java application built with Gradle. It includes securing the server by creating a non-root user and configuring basic application runtime.

---

## ✅ Step-by-Step Guide

### Step 1: Create a Droplet on DigitalOcean
- Log in to [DigitalOcean](https://cloud.digitalocean.com).
- Click **Create > Droplet**.
- Choose:
  - **Ubuntu** as the OS.
  - Datacenter region (closest to your users).
  - Enable SSH authentication or set a strong root password.
- Create the Droplet and note its public IP address.
- Open ports 22 and 7071

---

### Step 2: Connect to the Droplet via SSH
```bash
ssh root@<DROPLET_PUBLIC_IP>
```

---

### Step 3: Create and Configure a New Linux User
> Security best practice – avoid running applications as `root`

```bash
# Create a new user
adduser devuser

# Give sudo privileges
usermod -aG sudo devuser

```

Then test:
```bash
ssh devuser@<DROPLET_PUBLIC_IP>
```

---

### Step 4: Install Java and Gradle
```bash
# Update and install Java
sudo apt update && sudo apt install -y openjdk-17-jdk

# Verify Java
java -version

# Install Gradle dependencies
sudo apt install -y unzip wget

# Download and install Gradle manually
wget https://services.gradle.org/distributions/gradle-8.2.1-bin.zip -P /tmp
sudo unzip -d /opt/gradle /tmp/gradle-8.2.1-bin.zip
echo 'export PATH=$PATH:/opt/gradle/gradle-8.2.1/bin' >> ~/.bashrc
source ~/.bashrc

# Verify Gradle
gradle -v
```

---

### Step 5: Deploy Your Java Gradle App

#### Option A: Clone via Git
```bash
git clone https://github.com/TsembA/m5-java-react-example.git
cd m5-Cloud-IaC-DigitalOcean
```

#### Option B: Transfer with SCP
```bash
scp -r ./m5-Cloud-IaC-DigitalOcean devuser@<DROPLET_PUBLIC_IP>:~/m5-Cloud-IaC-DigitalOcean
```

---

### Step 6: Build and Run the Application
```bash
cd m5-Cloud-IaC-DigitalOcean

# Build the app
gradle build

# Run the app
java -jar build/libs/m5-Cloud-IaC-DigitalOcean.jar
```

To run it in the background:
```bash
nohup java -jar build/libs/m5-Cloud-IaC-DigitalOcean.jar &
```

---

## 🎯 Result

Your Java application is now deployed and running on a secure, production-grade Linux server hosted on DigitalOcean.



# Java-React Example

An example of how to use JS frontend to consume an endpoint written in Java.

## Frontend technologies

- [React](https://facebook.github.io/react/) - UI Library
- [Redux](http://redux.js.org/) - State container

## Additional information

This project is a part of a [presentation](https://docs.google.com/presentation/d/1-yZhsM43cyWWDVn6EUtK_wc39FAv-19_jwsKXlTe2o8/edit?usp=sharing)

Related projects:

- [react-intro](https://github.com/mendlik/react-intro) - Introduction to react and redux.
- [java-webpack-example](https://github.com/mendlik/java-webpack-example) - Advanced example showing how to use a module bundler in  a Java project.

Tip: [How to enable LiveReload in IntelliJ](http://stackoverflow.com/a/35895848/2284884)

<hr/>
Original project can be found here: https://github.com/pmendelski/java-react-example 
