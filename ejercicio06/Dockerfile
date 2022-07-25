FROM registry.redhat.io/redhat-openjdk-18/openjdk18-openshift:1.12-1.1655301789
WORKDIR /
ADD passwordapi.jar passwordapi.jar
EXPOSE 8080
CMD java -jar passwordapi.jar