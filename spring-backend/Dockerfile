FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /app

COPY pom.xml .
RUN  mvn -B dependency:go-offline

COPY /src src
RUN mvn -B clean package -DskipTests \
    && rm -rf /root/.m2/repository



FROM eclipse-temurin:17-jre

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser && \
    chown appuser:appgroup /app/app.jar && \
    rm -rf /var/cache/apk/*

USER appuser

CMD ["java", "-jar", "app.jar"]
