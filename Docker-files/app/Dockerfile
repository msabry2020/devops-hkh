FROM tomcat:9-jre11
ARG BUILD_ID
ARG BUILD_TIMESTAMP
RUN rm -rf /usr/local/tomcat/webapps/*
RUN curl -u 'admin:admin' -o /usr/local/tomcat/webapps/ROOT.war http://172.17.0.1:8081/repository/vprofile-release/QA/vproapp/$BUILD_ID-$BUILD_TIMESTAMP/vproapp$BUILD_ID-$BUILD_TIMESTAMP.war

EXPOSE 8080
CMD ["catalina.sh", "run"]