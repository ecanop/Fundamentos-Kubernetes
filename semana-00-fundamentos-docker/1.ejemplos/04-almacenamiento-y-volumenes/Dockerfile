FROM  python:3.11.18-alpine3.23

RUN apk upgrade --no-cache

# Usuario sin privilegios
RUN addgroup -g 10001 -S appgroup && \
    adduser -u 10001 -S appuser -G appgroup

WORKDIR /app

# Crear la carpeta de datos asignando permisos al usuario no-root
RUN mkdir -p /app/datos && chown -R appuser:appgroup /app/datos

COPY --chown=appuser:appgroup app.py .

ENV PORT=8080
ENV DATA_DIR="/app/datos"

USER appuser
EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget -q -O /dev/null http://localhost:8080/health || exit 1

CMD ["python", "app.py"]
