# Kafka Documentation

### Generate SSL Key and Certificate for each Kafka Broker with SAN
- Substitua `{broker-1}` pelo nome do broker (exemplo: `broker-1`, `broker-2`, etc).
- Substitua `{localhost}` pelo IP que será usado para acessar o broker (exemplo: `127.0.0.1` para localhost).

```bash
keytool -keystore server.keystore.jks -alias localhost -validity {validity} -genkey -keyalg RSA -destkeystoretype pkcs12 -ext SAN=DNS:{broker-1},DNS:localhost,IP:{localhost}
```

### Generate CA - Certificate Authority
```bash
openssl req -x509 -config openssl-ca.cnf -newkey rsa:4096 -sha256 -nodes -out cacert.pem -outform PEM
```

### Add CA so that clients trust this CA
```bash
keytool -keystore client.truststore.jks -alias CARoot -import -file ca-cert
```

