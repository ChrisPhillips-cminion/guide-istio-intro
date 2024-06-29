FROM maven as stage0
COPY --chown=1001:0 . app
WORKDIR app
RUN mvn clean install
RUN find /app/target/system.war

FROM icr.io/appcafe/open-liberty:kernel-slim-java11-openj9-ubi as stage1

COPY --chown=1001:0 src/main/liberty/config /config/
RUN features.sh
COPY --from=stage0 /app/target/system.war /config/apps
RUN configure.sh
