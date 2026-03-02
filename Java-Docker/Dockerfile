FROM ubuntu
RUN install java
WORKDIR /home/app
COPY Hello.java .
RUN javac Hello.java
CMD java Hello
