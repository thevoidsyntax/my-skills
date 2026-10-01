---
name: observability
description: "Full-stack observability standards including logging, tracing, and metrics patterns."
version: "1.0"
---

# OBSERVABILITY MODULE

Kamu adalah Observability Specialist. Gunakan rules ini untuk setiap aspek observability dalam proyek.

---

## 1. THE THREE PILLARS

### Logging
- **Structured Logging:** Selalu gunakan JSON format untuk log yang machine-readable
- **Log Levels:** ERROR, WARN, INFO, DEBUG, TRACE - gunakan dengan tepat
- **Correlation:** Setiap request harus punya correlation ID yang propagates ke semua service
- **Context:** Include request ID, user ID, trace ID di setiap log entry

### Metrics
- **RED Metrics:**
  - **Rate:** Request per second
  - **Errors:** Error rate percentage
  - **Duration:** Latency (p50, p95, p99)
- **USE Metrics:**
  - **Utilization:** Resource usage percentage
  - **Saturation:** How full the queue is
  - **Errors:** Error count
- **Business Metrics:**
  - Conversion rates
  - User actions
  - Revenue metrics

### Tracing
- **Distributed Tracing:** Trace request dari awal hingga akhir
- **Span:** Setiap operation harus punya span dengan timing
- **Propagation:** Trace ID harus propagate via headers
- **Sampling:** Sample high-traffic endpoints (1-10%)

---

## 2. LOGGING STANDARDS

### Log Format (JSON)
```json
{
  "timestamp": "2024-01-15T10:30:00.000Z",
  "level": "info",
  "message": "User login successful",
  "correlationId": "abc123",
  "userId": "user_123",
  "service": "auth-service",
  "environment": "production",
  "metadata": {
    "ip": "192.168.1.1",
    "userAgent": "Mozilla/5.0..."
  }
}
```

### Log Levels Usage
| Level | When to Use |
|-------|-------------|
| ERROR | Something failed, needs attention |
| WARN | Something unexpected, but handled |
| INFO | Important business events |
| DEBUG | Detailed troubleshooting info |
| TRACE | Very verbose, development only |

### Log Best Practices
- Never log sensitive data (passwords, tokens, PII)
- Use meaningful log messages
- Include context for debugging
- Log errors with stack traces
- Use appropriate log rotation

---

## 3. METRICS IMPLEMENTATION

### Required Metrics per Service

#### HTTP/REST APIs
```
http_requests_total{method, route, status_code}
http_request_duration_seconds{method, route}
http_request_size_bytes
http_response_size_bytes
```

#### Business Metrics
```
campaign_messages_sent_total{campaign_id, status}
campaign_messages_failed_total{campaign_id, reason}
blast_duration_seconds{campaign_id}
contacts_imported_total{source}

whatsapp_connection_status{connected, disconnected}
whatsapp_messages_sent_total
whatsapp_messages_failed_total
```

#### System Metrics
```
process_cpu_seconds_total
process_memory_bytes
nodejs_eventloop_lag_seconds
active_connections_total
database_connections_active
```

### Prometheus Metrics Endpoint
```
GET /metrics
Content-Type: text/plain

# HELP http_requests_total Total HTTP requests
# TYPE http_requests_total counter
http_requests_total{method="GET",route="/api/health",status="200"} 12345
```

---

## 4. HEALTH CHECKS

### Three-Level Health Checks

#### Liveness Probe (Is the process alive?)
```javascript
app.get('/health/live', (req, res) => {
  res.json({ status: 'alive', timestamp: new Date().toISOString() });
});
```
- Should always return 200 if process is running
- Don't check dependencies here

#### Readiness Probe (Can it serve traffic?)
```javascript
app.get('/health/ready', async (req, res) => {
  const checks = {
    database: await checkDatabase(),
    whatsapp: await checkWhatsApp(),
    redis: await checkRedis()
  };
  
  const allHealthy = Object.values(checks).every(Boolean);
  
  if (allHealthy) {
    res.json({ status: 'ready', checks });
  } else {
    res.status(503).json({ status: 'not_ready', checks });
  }
});
```
- Check all dependencies
- Return 503 if can't serve traffic

#### Startup Probe (Is initialization complete?)
```javascript
app.get('/health/started', (req, res) => {
  if (initializationComplete) {
    res.json({ status: 'started' });
  } else {
    res.status(503).json({ status: 'starting' });
  }
});
```
- For slow-starting applications

---

## 5. DISTRIBUTED TRACING

### Correlation ID
```javascript
// Middleware to add correlation ID
app.use((req, res, next) => {
  req.correlationId = req.headers['x-correlation-id'] || 
                      crypto.randomUUID();
  res.setHeader('X-Correlation-ID', req.correlationId);
  next();
});
```

### Request Logging
```javascript
app.use((req, res, next) => {
  const start = Date.now();
  
  res.on('finish', () => {
    logger.info('Request completed', {
      correlationId: req.correlationId,
      method: req.method,
      path: req.path,
      statusCode: res.statusCode,
      duration: Date.now() - start,
      userAgent: req.headers['user-agent']
    });
  });
  
  next();
});
```

### Trace Propagation Headers
```
X-Correlation-ID: abc123
X-Request-ID: def456
X-B3-TraceId: 4bf92f3577b34da6a3ce929d0e0e4736
X-B3-SpanId: 00f067aa0ba902b7
X-B3-ParentSpanId: 4bf92f3577b34da6
```

---

## 6. ALERTING RULES

### SLO Definitions

| Service | Availability | Latency (p99) |
|---------|--------------|---------------|
| API Gateway | 99.9% | < 500ms |
| WhatsApp Service | 99.5% | < 2s |
| Database | 99.9% | < 100ms |

### Alert Severity

#### P1 - Critical (Immediate action)
```
- Service completely down
- Data loss detected
- Security breach
```

#### P2 - High (Action within 1 hour)
```
- Error rate > 5%
- Latency increase > 50%
- Resource usage > 90%
```

#### P3 - Medium (Action within 4 hours)
```
- Error rate > 1%
- Non-critical service degraded
- Disk space > 80%
```

#### P4 - Low (Schedule fix)
```
- Minor performance degradation
- Non-critical logs showing errors
- Certificate expiring in 7 days
```

### Example Alert Rules (Prometheus)
```yaml
groups:
  - name: whatsapp-blast
    rules:
      - alert: HighErrorRate
        expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.05
        for: 5m
        labels:
          severity: high
        annotations:
          summary: High error rate detected
          
      - alert: WhatsAppDisconnected
        expr: whatsapp_connection_status == 0
        for: 1m
        labels:
          severity: critical
          
      - alert: HighLatency
        expr: histogram_quantile(0.99, http_request_duration_seconds) > 2
        for: 5m
        labels:
          severity: medium
```

---

## 7. DASHBOARDS

### Recommended Dashboard Panels

#### Overview Dashboard
```
┌─────────────────────────────────────────────────────────────┐
│  Service Overview                                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐          │
│  │ Requests    │ │ Error Rate  │ │ Latency p99 │          │
│  │ 1,234/min   │ │ 0.5%        │ │ 245ms       │          │
│  └─────────────┘ └─────────────┘ └─────────────┘          │
│                                                             │
│  ┌───────────────────────────────────────────────────────┐ │
│  │ Request Rate (last 24h)                               │ │
│  │                                                       │ │
│  │     █                                               │ │
│  │   █ █     █                                         │ │
│  │ █ █ █ █ █ █ █                                       │ │
│  │ ───────────────────────────────────────────────     │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### WhatsApp Service Dashboard
```
┌─────────────────────────────────────────────────────────────┐
│  WhatsApp Service Metrics                                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Connection Status: [●] Connected                            │
│                                                             │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐          │
│  │ Sent Today  │ │ Failed Today │ │ Pending     │          │
│  │ 234         │ │ 12          │ │ 56          │          │
│  └─────────────┘ └─────────────┘ └─────────────┘          │
│                                                             │
│  Blast Queue:                                                │
│  - Campaign "Promo July": Running (45%)                     │
│  - Campaign "GrabKios": Pending (150 contacts)              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 8. OPENTELEMETRY INTEGRATION

### Basic Setup
```javascript
const { NodeSDK } = require('@opentelemetry/sdk-node');
const { JaegerExporter } = require('@opentelemetry/exporter-jaeger');
const { HttpInstrumentation } = require('@opentelemetry/instrumentation-http');
const { ExpressInstrumentation } = require('@opentelemetry/instrumentation-express');

const sdk = new NodeSDK({
  serviceName: 'whatsapp-blast',
  traceExporter: new JaegerExporter({
    endpoint: 'http://jaeger:14268/api/traces'
  }),
  instrumentations: [
    new HttpInstrumentation(),
    new ExpressInstrumentation()
  ]
});

sdk.start();
```

### Custom Spans
```javascript
const { trace } = require('@opentelemetry/api');

const tracer = trace.getTracer('whatsapp-blast');

async function sendBlast(campaignId, contacts) {
  const span = tracer.startSpan('blast.send');
  span.setAttribute('campaign.id', campaignId);
  span.setAttribute('contacts.count', contacts.length);
  
  try {
    for (const contact of contacts) {
      await sendMessage(contact);
    }
    span.setStatus({ code: SpanStatusCode.OK });
  } catch (error) {
    span.setStatus({ code: SpanStatusCode.ERROR });
    span.recordException(error);
    throw error;
  } finally {
    span.end();
  }
}
```

---

## 9. LOG AGGREGATION

### ELK Stack Integration
```javascript
// Winston with Elasticsearch transport
const winston = require('winston');
const ElasticsearchTransport = require('winston-elasticsearch');

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  transports: [
    new ElasticsearchTransport({
      level: 'info',
      index: 'whatsapp-blast-logs',
      indexPrefix: 'logs-YYYY.MM.DD',
      transformer: logData => ({
        '@timestamp': logData.timestamp || new Date().toISOString(),
        message: logData.message,
        severity: logData.level,
        fields: logData.meta
      })
    })
  ]
});
```

### Loki Integration (Grafana)
```javascript
// Winston with Loki transport
const LokiTransport = require('winston-loki');

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  transports: [
    new LokiTransport({
      host: 'http://loki:3100',
      labels: {
        app: 'whatsapp-blast',
        environment: process.env.NODE_ENV
      }
    })
  ]
});
```

---

## 10. ERROR TRACKING

### Sentry Integration
```javascript
const Sentry = require('@sentry/node');

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,
  tracesSampleRate: 0.1,
  integrations: [
    new Sentry.Integrations.Express({ app }),
    new Sentry.Integrations.Http({ breadcrumbs: true })
  ]
});

// Error handler
app.use(Sentry.Handlers.errorHandler());

// Manual error capture
try {
  await riskyOperation();
} catch (error) {
  Sentry.captureException(error, {
    tags: { campaign_id: campaignId },
    extra: { contacts_count: contacts.length }
  });
  throw error;
}
```

### Error Categories
```javascript
const ErrorCategory = {
  VALIDATION: 'validation_error',
  AUTHENTICATION: 'auth_error',
  AUTHORIZATION: 'authz_error',
  NOT_FOUND: 'not_found',
  RATE_LIMIT: 'rate_limit',
  WHATSAPP_API: 'whatsapp_error',
  DATABASE: 'database_error',
  EXTERNAL_SERVICE: 'external_error',
  INTERNAL: 'internal_error'
};
```

---

## 11. PERFORMANCE MONITORING

### Request Performance
```javascript
// Add to routes
app.use((req, res, next) => {
  const start = process.hrtime.bigint();
  
  res.on('finish', () => {
    const end = process.hrtime.bigint();
    const durationNs = Number(end - start);
    const durationMs = durationNs / 1_000_000;
    
    metricsCollector.observe(
      'http_request_duration_ms',
      { method: req.method, route: req.route?.path || 'unknown' },
      durationMs
    );
  });
  
  next();
});
```

### WhatsApp Performance
```javascript
const whatsappMetrics = {
  // Message sending metrics
  sendDuration: new Histogram({
    name: 'whatsapp_message_send_duration_ms',
    help: 'Duration of message send operations',
    buckets: [100, 250, 500, 1000, 2000, 5000]
  }),
  
  // Queue metrics
  queueSize: new Gauge({
    name: 'whatsapp_blast_queue_size',
    help: 'Current blast queue size'
  }),
  
  // Connection metrics
  reconnectCount: new Counter({
    name: 'whatsapp_reconnect_total',
    help: 'Total WhatsApp reconnection attempts'
  })
};
```

---

## 12. ON-CALL BEST PRACTICES

### Runbook Template
```markdown
# Runbook: WhatsApp Service Down

## Symptoms
- WhatsApp connection status shows "disconnected"
- Blast operations failing with "connection error"
- Health check returning 503

## Diagnosis
1. Check WhatsApp Web session status
   ```
   curl localhost:3000/api/status
   ```

2. Check session files
   ```
   ls -la data/sessions/
   ```

3. Check logs for errors
   ```
   tail -f data/logs/server.log | grep -i error
   ```

## Resolution
1. If session corrupted:
   ```bash
   rm -rf data/sessions/*
   systemctl restart whatsapp-blast
   # User must re-scan QR code
   ```

2. If rate limited by WhatsApp:
   - Wait 1 hour before retry
   - Check WhatsApp official status
   - Consider using backup device

3. If persistent issues:
   - Escalate to senior engineer
   - Consider failover to backup instance

## Prevention
- Monitor connection status 24/7
- Set up alert for disconnection
- Keep backup WhatsApp device ready
```

### Escalation Matrix
| Severity | Response Time | Escalation |
|----------|---------------|------------|
| P1 | 15 minutes | On-call → Team Lead → CTO |
| P2 | 1 hour | On-call → Team Lead |
| P3 | 4 hours | On-call |
| P4 | Next business day | Ticket system |

---

**Invok:** `/observability` | **Priority:** HIGH | **Version:** 1.0
