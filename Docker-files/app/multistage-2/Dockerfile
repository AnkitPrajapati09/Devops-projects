FROM eclipse-temurin:17-jdk AS build_image
RUN apt update && apt install git maven -y
RUN git clone -b docker https://github.com/devopshydclub/vprofile-project.git
RUN cd vprofile-project && mvn install


FROM tomcat:8-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Ankit"

RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=build_image vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
WORKDIR /usr/local/tomcat/
VOLUME /usr/local/tomcat/webapps
