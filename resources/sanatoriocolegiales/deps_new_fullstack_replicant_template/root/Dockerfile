FROM eclipse-temurin:24-ubi9-minimal
WORKDIR /app

RUN groupadd -g 1001 appgroup && useradd -u 1001 -g appgroup -s /bin/sh -m appuser
RUN mkdir -p /app/logs && chown -R appuser:appgroup /app && chmod 755 /app/logs

VOLUME [ "/app/logs" ]

COPY --chown=appuser:appgroup /target/*.jar /app/app.jar

RUN echo '#!/bin/sh' > /entrypoint.sh && \
    echo 'chown -R appuser:appgroup /app/logs' >> /entrypoint.sh && \
    echo 'chmod 755 /app/logs' >> /entrypoint.sh && \
    echo 'exec runuser -u appuser -- "$@"' >> /entrypoint.sh && \
    chmod +x /entrypoint.sh

EXPOSE 4500
ENV LOGPATH="/app/logs/logs.edn"

ENTRYPOINT ["/entrypoint.sh"]
CMD [ "java", "-jar", "app.jar"]