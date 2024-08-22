FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && \
    apt install maven -y && \
    git clone -b docker https://github.com/devopshydclub/vprofile-project.git && \
    cd devops-hkh && mvn install


FROM tomcat:9-jre11
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ['catalina.sh', "run"]