FROM tomcat:9-jre11
RUN rm -rf /usr/local/tomcat/webapps/*
RUN curl -u 'admin:admin' -o /usr/local/tomcat/webapps/ROOT.war http://172.17.0.1:8081/repository/vprofile-release/QA/vproapp/4-24-10-14/vproapp-4-24-10-14.war

EXPOSE 8080
CMD ["catalina.sh", "run"]