ARG ELK_VERSION

# https://www.docker.elastic.co/
FROM docker.elastic.co/logstash/logstash:${ELK_VERSION}

# Add your logstash plugins setup here
# Example: RUN logstash-plugin install logstash-filter-json

# Kompose workaround
COPY config /usr/share/logstash/config/
COPY pipeline /usr/share/logstash/pipeline/
COPY jdbc/mysql-connector-java.jar /usr/share/java/mysql-connector-java.jar
