FROM openjdk:8
ENV TZ GMT

ENTRYPOINT ["java","-jar", "/usr/share/app/application.jar"]

# Add the service itself
ARG JAR_FILE
ADD target/${JAR_FILE} /usr/share/app/application.jar