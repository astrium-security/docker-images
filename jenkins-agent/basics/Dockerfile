# Start with the official Ubuntu base image 
FROM ubuntu:23.04

# Avoid any interactive dialog during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Install prerequisites: Java, Git, and other utilities
RUN apt-get update && \
    apt-get install -y openjdk-20-jdk git curl unzip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Download and install the Jenkins agent jar
ARG JENKINS_REMOTING_VERSION=4.14
RUN curl -fsSLo /usr/share/jenkins/agent.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${JENKINS_REMOTING_VERSION}/remoting-${JENKINS_REMOTING_VERSION}.jar && \
    chmod 755 /usr/share/jenkins && \
    chmod 644 /usr/share/jenkins/agent.jar

# Add user jenkins
RUN useradd -m -d /home/jenkins jenkins

# Switch to the jenkins user
USER jenkins

# Set the entrypoint
ENTRYPOINT ["java", "-jar", "/usr/share/jenkins/agent.jar"]
