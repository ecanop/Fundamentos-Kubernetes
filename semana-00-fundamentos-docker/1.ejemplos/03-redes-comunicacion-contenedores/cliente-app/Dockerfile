FROM  python:3.11.18-alpine3.23

RUN apk upgrade --no-cache

RUN addgroup -g 10001 -S appgroup && \
    adduser -u 10001 -S appuser -G appgroup

WORKDIR /app
COPY --chown=appuser:appgroup app.py .

ENV PORT=8081
ENV BACKEND_HOST="greca-central"
ENV BACKEND_PORT=8080
ENV NOMBRE_CLIENTE="carrito-san-antonio"

USER appuser
EXPOSE 8081

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget -q -O /dev/null http://localhost:8081/health || exit 1

CMD ["python", "app.py"]
