# Multistage

# Stage1:
FROM openjdk:8 AS BUILD_IMAGE
# we need openjdk to run maven to build 
WORKDIR /usr/src/app/
RUN apt update && apt install maven -y
COPY ./ /usr/src/app/
# Copy the entire javaapi folder contents into /usr/src/app of this builder container
RUN mvn install -DskipTests
# Maven will build the artifact from the java source code



# Stage2: 
FROM openjdk:8

WORKDIR /usr/src/app/
COPY --from=BUILD_IMAGE /usr/src/app/target/book-work-0.0.1-SNAPSHOT.jar ./book-work-0.0.1.jar
# Copy the artifact from Stage1 builder container into /usr/src/app/ directory. This is java
# so the artifact file is a .jar file.  The .jar file needs to be renamed as book-work-0.0.1.jar

EXPOSE 9000
ENTRYPOINT ["java","-jar","book-work-0.0.1.jar"]
# this will run java -jar book-work-0.0.1.jar to start the java books api application on this container
# The applicaton will be exposed to run on port 9000
# Test
