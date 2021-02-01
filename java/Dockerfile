#docker build -t lucianobrd/java java/
#docker run -it --rm --name java lucianobrd/java

FROM openjdk:7

COPY ./app /usr/src/app
WORKDIR /usr/src/app
RUN javac Main.java
CMD ["java", "Main"]