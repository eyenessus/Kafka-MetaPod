# Kafka Documentation

## Create database and serial number file
```bash
echo 01 > serial.txt
touch index.txt
```

### Generate CA - Certificate Authority
```bash
openssl req -x509 -config openssl-ca.cnf -newkey rsa:4096 -sha256 -nodes -out cacert.pem -outform PEM
```

### Import CA to client truststore, this add CA so that clients trust this CA
```bash
keytool -keystore client.truststore.jks -alias CARoot -import -file cacert.pem
```

### Generate SSL Key and Certificate for each Kafka Broker with SAN Temporary
- Substitua `{broker-1}` pelo nome do broker (exemplo: `broker-1`, `broker-2`, etc).
- Substitua `{localhost}` pelo IP que será usado para acessar o broker (exemplo: `127.0.0.1` para localhost).

```bash
keytool -keystore {broker-1}.keystore.jks -alias {broker-1} -validity {validity} -genkey -keyalg RSA -storetype pkcs12 -ext SAN=DNS:broker-1,DNS:localhost,IP:127.0.0.1
```

## Generate CSR CERTIFICATE SIGNING REQUEST of Broker
```bash
keytool -keystore {broker-1}.keystore.jks -alias {broker-1} -certreq -file {broker-1}.csr -ext SAN=DNS:broker-1,DNS:localhost,IP:127.0.0.1
```

### Sign it with the CA
```bash
openssl ca -config openssl-ca.cnf -policy signing_policy -extensions signing_req -out {broker-1}.crt -infiles {broker-1}.csr
```

## Need to import both the certificate of the CA and the signed certificate into the keystore
```bash
keytool -keystore broker/{broker-1}.keystore.jks -alias CARoot -import -file ca/cacert.pem
keytool -keystore {keystore} -alias {broker-1}.keystore.jks -import -file broker/{broker-1}.crt
```

### Provider truststore to each brokers it should have all CA certificates that clients keys were signed by.
```bash
keytool -keystore {broker-1}.truststore.jks -alias CARoot -import -file cacert.pem
```

