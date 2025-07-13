# Kafka Documentation

## Security

### Generate SSL Key and Certificate for each Kafka Broker with SAN
```bash
    keytool -keystore server.keystore.jks -alias localhost -validity {validity} -genkey -keyalg RSA -ext SAN=DNS:{broker-1}
```
