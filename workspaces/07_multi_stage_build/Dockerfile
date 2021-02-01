# 1st stage
FROM mcr.microsoft.com/java/jdk:8-zulu-alpine AS derleyici
COPY /source /usr/src/uygulama
WORKDIR /usr/src/uygulama
RUN javac uygulama.java
# 2nd stage
FROM mcr.microsoft.com/java/jre:8-zulu-alpine
WORKDIR /uygulama
COPY --from=derleyici /usr/src/uygulama .
CMD ["java","uygulama"]