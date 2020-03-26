# Apache Knox - Proxying Apache NiFi
### Generating SSL/TLS Certificates with Apache NiFi TLS Toolkit
Термины и определения:
- Trust Store - цепочка сертификатов доверенных центров сертификации. Вот так можно посмотреть, какие сертификаты лежат в truststore: _keytool -list -keystore truststore.jks_
- Key Store - ключи 
- 

Создание ключа:
```sh
[root@dtrubenkov-platform2 bin]# ./tls-toolkit.sh standalone --hostnames dtrubenkov-platform2  --isOverwrite --trustStorePassword truststore --keyStorePassword nifi --keyStoreType jks
2020/03/26 12:01:17 INFO [main] org.apache.nifi.toolkit.tls.standalone.TlsToolkitStandaloneCommandLine: No nifiPropertiesFile specified, using embedded one.
2020/03/26 12:01:17 INFO [main] org.apache.nifi.toolkit.tls.standalone.TlsToolkitStandalone: Running standalone certificate generation with output directory ../bin
2020/03/26 12:01:18 INFO [main] org.apache.nifi.toolkit.tls.standalone.TlsToolkitStandalone: Generated new CA certificate ../bin/nifi-cert.pem and key ../bin/nifi-key.key
2020/03/26 12:01:18 INFO [main] org.apache.nifi.toolkit.tls.standalone.TlsToolkitStandalone: Writing new ssl configuration to ../bin/dtrubenkov-platform2
2020/03/26 12:01:19 INFO [main] org.apache.nifi.toolkit.tls.standalone.TlsToolkitStandalone: Successfully generated TLS configuration for dtrubenkov-platform2 1 in ../bin/dtrubenkov-platform2
2020/03/26 12:01:19 INFO [main] org.apache.nifi.toolkit.tls.standalone.TlsToolkitStandalone: No clientCertDn specified, not generating any client certificates.
2020/03/26 12:01:19 INFO [main] org.apache.nifi.toolkit.tls.standalone.TlsToolkitStandalone: tls-toolkit standalone completed successfully
```
__Важное:__
- NiFi does not perform user authentication over HTTP. Using HTTP, all users will be granted all roles.
- NiFi can only be configured for username/password, OpenId Connect, or Apache Knox at a given time. It does not support running each of these concurrently. NiFi will require client certificates for authenticating users over HTTPS if none of these are configured.
- 

 openssl x509 -inform der -in admin.cer -noout -text
https://serverfault.com/questions/215606/how-do-i-view-the-details-of-a-digital-certificate-cer-file

