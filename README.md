# Kafka Documentation

### Generate SSL Key and Certificate for each Kafka Broker with SAN
- Substitua `{broker-1}` pelo nome do broker (exemplo: `broker-1`, `broker-2`, etc).
- Substitua `{localhost}` pelo IP que será usado para acessar o broker (exemplo: `127.0.0.1` para localhost).

```bash
keytool -keystore {broker-1}.keystore.jks -alias {broker-1} -validity 365 -genkey -keyalg RSA -storetype pkcs12
```
> Substitua `{broker-1}` pelo nome do broker desejado. O arquivo gerado será `{broker-1}.keystore.jks`.
```

### Generate CA - Certificate Authority
```bash
openssl req -x509 -config openssl-ca.cnf -newkey rsa:4096 -sha256 -nodes -out cacert.pem -outform PEM
```

### Add CA so that clients trust this CA
```bash
keytool -keystore client.truststore.jks -alias CARoot -import -file ca-cert
```

