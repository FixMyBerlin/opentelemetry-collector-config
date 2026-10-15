# OpenTelemetry Collector – Vorlage mit OneUptime

Diese Vorlage zeigt, wie der [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/) per Docker Compose betrieben werden kann. Als Exporter wird [OneUptime](https://oneuptime.com/) verwendet, aber jeder andere OTLP-kompatible Exporter (z. B. Grafana Cloud, Jaeger, Prometheus) lässt sich durch Anpassung des `exporters`-Blocks in `config.yaml` einsetzen.

## Enthaltene Integrationen

| Receiver | Daten |
|---|---|
| `host_metrics` | CPU-, Arbeitsspeicher- und Dateisystem-Metriken des Host-Systems |
| `file_log/docker` | Container-Logs aus dem Docker-JSON-Log-Treiber |
| `otlp` (gRPC + HTTP) | Empfang externer Traces, Metriken und Logs von eigenen Diensten |

## Schnellstart

1. `.env.example` nach `.env` kopieren und Werte eintragen:
   ```bash
   OTEL_SERVICE_INSTANCE_ID=SERVICE-ID-HERE   # z. B. Hostname oder UUID
   ONEUPTIME_TOKEN=YOUR-SECRET-HERE           # Ingest-Token aus der OneUptime-Projektverwaltung
   ```
   Beachte, dass das Ingest Token pro Projekt festgelegt ist. Die `.env` bleibt auf dem Server und gehört nicht ins Repo.
   Die OTLP-Ports sind standardmäßig nur über `127.0.0.1` erreichbar (`OTEL_BIND_ADDRESS` in der `.env` ändert das).

2. Collector starten:
   ```bash
   docker compose up -d
   ```

Auf dem VPS muss der Port 80/443 offen sein.
