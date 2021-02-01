# Installing OS
FROM ubuntu:18.04
# Updating OS
RUN apt-get update -y
# Installing JRE
RUN apt-get install default-jre -y
# Creating a directory in the image directory
WORKDIR /merhaba
# Copying contents of an app to the image. myapp is a folder in which Dockerfile exists.
COPY /myapp .
# Run the command that was run just after creating a container
CMD ["java","merhaba"]
