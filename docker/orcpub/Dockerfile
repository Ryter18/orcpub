FROM clojure:openjdk-8-lein as builder
MAINTAINER daemonsthere@gmail.com

# Build cache layer
ADD ./lib/ /root/.m2/repository/
WORKDIR /orcpub
COPY project.clj /orcpub/
RUN lein deps

ADD ./ /orcpub
RUN printenv &&\
	lein uberjar

FROM openjdk:8-jre-alpine as runner
MAINTAINER daemonsthere@gmail.com

COPY --from=builder /orcpub/target/orcpub.jar /orcpub.jar

ENTRYPOINT ["java", "-jar"]
CMD ["/orcpub.jar"]
