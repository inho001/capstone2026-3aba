# 1단계: 빌드 스테이지 (Maven 포함 이미지 사용)
FROM maven:3.8.4-openjdk-17 AS build
WORKDIR /app
# 프로젝트 소스 복사
COPY . .
# .jar 파일 생성
RUN mvn clean package -DskipTests

# 2단계: 실행 스테이지 (가벼운 JRE 이미지 사용)
FROM eclipse-temurin:17-jdk-jammy
WORKDIR /app
# 빌드 스테이지에서 생성된 jar만 쏙 빼오기
COPY --from=build /app/target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]