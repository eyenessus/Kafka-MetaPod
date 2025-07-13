# Kafka Documentation

## Security

### Generate SSL Key and Certificate for each Kafka Broker
```bash
keytool -keystore server.keystore.jks -alias localhost -validity 730 -genkey -keyalg RSA
```
