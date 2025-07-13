# Kafka Documentation

## Security
### Generate SSL Key and Certificate for each Kafka Broker with SAN
#### Replace `{broker-1}` with the name of the broker
```bash
keytool -keystore server.keystore.jks -alias localhost -validity {validity} -genkey -keyalg RSA -ext SAN=DNS:{broker-1}
```

### Generate CA - Certificate Authority
```bash
openssl req -new -x509 -keyout ca-key -out ca-cert -days 365
```

### Add CA so that clients trust this CA
```bash
keytool -keystore client.truststore.jks -alias CARoot -import -file ca-cert
```

