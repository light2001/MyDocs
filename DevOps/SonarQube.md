## SonarQube

## SonqrQube Server

## 下面是docker compose ,通过这个脚本就能一键启动SonarQube的Docker容器
~~~
version: "3"

services:
  # SonarQube Database Service
  db:
    image: postgres:15 # Use a specific stable version like 15
    container_name: sonarqube_db
    environment:
      # !!! IMPORTANT: Change these default values for security !!!
      POSTGRES_USER: sonarqube
      POSTGRES_PASSWORD: your_strong_password # <-- CHANGE THIS PASSWORD
      POSTGRES_DB: sonarqube
    volumes:
      - db_data:/var/lib/postgresql/data # Persist database data
    restart: unless-stopped # Auto-restart unless explicitly stopped

  # SonarQube Application Service
  sonarqube:
    image: sonarqube:lts # Use the Long Term Support (LTS) version
    container_name: sonarqube_app
    ports:
      - "9000:9000" # Map host port 9000 to SonarQube container port 9000
    environment:
      # Configure SonarQube to connect to the PostgreSQL database
      # jdbc:postgresql://<db_service_name>:<db_port>/<db_name>
      SONARQUBE_JDBC_URL: jdbc:postgresql://db:5432/sonarqube
      # !!! IMPORTANT: Use the same user and password as the database service !!!
      SONARQUBE_JDBC_USERNAME: sonarqube
      SONARQUBE_JDBC_PASSWORD: your_strong_password # <-- USE THE SAME PASSWORD
      # Configure Elasticsearch memory for SonarQube (adjust based on your resources)
      # Minimum 2GB RAM is generally recommended for SonarQube
      SONAR_SEARCH_JAVA_OPTS: "-Xmx1024m -Xms1024m -XX:+HeapDumpOnOutOfMemoryError" # Example: 1GB heap
    volumes:
      - sonarqube_data:/opt/sonarqube/data # Persist SonarQube data
      - sonarqube_extensions:/opt/sonarqube/extensions # Persist plugins and extensions
      - sonarqube_logs:/opt/sonarqube/logs # Persist logs
    depends_on:
      - db # Ensure database starts before SonarQube
    restart: unless-stopped

# Define named volumes for data persistence
volumes:
  db_data:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_logs:

~~~


## Sonar Lint


## Sonar Scanner


