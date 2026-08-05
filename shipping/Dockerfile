#
# Build Stage
#
FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /opt/shipping

COPY pom.xml .

RUN mvn dependency:go-offline

COPY src ./src

RUN mvn clean package -DskipTests

#
# Runtime Stage
#
FROM eclipse-temurin:21-jre

WORKDIR /opt/shipping

EXPOSE 8080

ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

CMD ["java","-Xms256m","-Xmx768m","-jar","shipping.jar"]
