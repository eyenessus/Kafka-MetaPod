# Kafka Documentation

## Security
### Generate SSL Key and Certificate for each Kafka Broker with SAN
#### Replace `{broker-1}` with the name of the broker
```bash
keytool -keystore server.keystore.jks -alias localhost -validity {validity} -genkey -keyalg RSA -ext SAN=DNS:{broker-1}
```

### Generate CA - Certificate Authority
```bash
openssl req -x509 -config openssl-ca.cnf -newkey rsa:4096 -sha256 -nodes -out cacert.pem -outform PEM
```

### Add CA so that clients trust this CA
```bash
keytool -keystore client.truststore.jks -alias CARoot -import -file ca-cert
```

