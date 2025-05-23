FROM openjdk:17-jdk-bullseye
WORKDIR /app
COPY LogyeAPI-0.0.1-Demo.jar app.jar

RUN mkdir -p /app/logs

# Filebeat 설치
RUN apt-get update && \
    apt-get install -y wget gnupg curl && \
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add - && \
    echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" > /etc/apt/sources.list.d/elastic-8.x.list && \
    apt-get update && \
    apt-get install -y filebeat && \
    rm -rf /var/lib/apt/lists/*

# Filebeat 설정 복사
COPY filebeat.yml /etc/filebeat/filebeat.yml

CMD java -jar app.jar & filebeat -e
