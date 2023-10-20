FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/stephanekechi/vprofile-project.git
RUN cd vprofile-project && git checkout containers && mvn clean install

FROM tomcat:9-jre11
RUN rm -rf /user/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/*.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]