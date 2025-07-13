# Kafka Documentation

## Security
### Generate SSL Key and Certificate for each Kafka Broker with SAN
#### Replace: {broker-1} with the name of the broker
```bash
keytool -keystore server.keystore.jks -alias localhost -validity {validity} -genkey -keyalg RSA -ext SAN=DNS:{broker-1}
```

### Generate CA - CERTIFICATE AUTHORITY
```bash
openssl req -new -x509 -keyout ca-key -out ca-cert -days 365
```
