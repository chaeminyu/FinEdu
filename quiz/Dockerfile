FROM --platform=linux/arm64/v8 eclipse-temurin:17

WORKDIR /app

# backend 디렉토리의 파일들을 복사
COPY build.gradle .
COPY settings.gradle .
COPY gradlew .
COPY gradle/ gradle/
COPY common/ common/
COPY quiz/ quiz/

# Gradle 실행 권한 설정
RUN chmod +x ./gradlew

# 프로젝트 빌드
RUN ./gradlew :quiz:build -x test

# JAR 파일 이름 변경
RUN mv quiz/build/libs/*.jar app.jar

# cryptography 패키지 설치
RUN apt-get update && apt-get install -y \
    python3-pip \
    && pip3 install --break-system-packages cryptography

EXPOSE 8082
ENTRYPOINT ["java", "-jar", "app.jar"]