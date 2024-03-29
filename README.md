![wso2](https://ticxar.co/wp-content/uploads/2019/12/apimngr.png)
# wso2
#### for WSO2 Services (AM, IS, Analytics) ####

***Add certificates to the store***
```bash
apt install openjdk-11-jre-headless
```
1. The first launch with default settings, then change the configs
2. Get ready-made certificates
```bash
openssl pkcs12 -export -in domen.crt -inkey domen.key -name "*.domen.com" -certfile certificate_ca.crt -out domen.pfx
```
```bash
keytool -importkeystore -srckeystore domen.pfx -srcstoretype pkcs12 -destkeystore domen.jks -deststoretype JKS
```
2. Ready certificates domain.jks put /home/wso2carbon/wso2am-4.1.0/repository/resources/security/
```bash
cp wso2-config-volume/*.jks wso2am-4.1.0/repository/resources/security/
```
3. deployment.toml file - change the name to the desired certificate store
```toml
[keystore.tls]
file_name =  "domen.jks"
type =  "JKS"
password =  "wso2carbon"
alias =  "*.domen.com"
key_password =  "wso2carbon"
```
```bash
docker restart wso2_am
```
#### MySQL database connection
Configure ---> Datasources ---> Add Datasource

**The class name of the JDBC driver to use. Make sure to copy the JDBC driver relevant to the database engine to the <PRODUCT_HOME>/repository/components/lib/ directory. For example, if you are using MySQL, specify com.mysql.jdbc.Driver as the driver and copy mysql-connector-java-5.XX-bin.jar file to this directory. If you do not copy the driver to this directory when you create the datasource, you will get an exception similar to Cannot load JDBC driver class com.mysql.jdbc.Driver.**

https://mvnrepository.com/artifact/mysql/mysql-connector-java

```bash
cp wso2-config-volume/mysql-connector-j-8.0.32.jar wso2am-4.1.0/repository/components/lib/
```
![image](https://user-images.githubusercontent.com/86954730/222174542-3cf461ce-be36-4cc4-9cbd-278e1c6c605f.png)
```yml
docker inspect -f "{{ .Config.Env }}" wso2_am
```
```yml
docker commit --change "ENV DEBUG=true" wso2_am tag/wso2image:version1
```

So that’s it. Access all the URLs of WSO2 to confirm everything is working fine.
```
https://<IP or Hostname>:9443/carbon

https://<IP or Hostname>:9443/publisher

https://<IP or Hostname>:9443/devportal

https://<IP or Hostname>:9443/admin

http://<IP or Hostname>:8082 ---- connect to BD h2
```

___Useful links:___

https://medium.com/@himashaguruge/using-keycloak-as-an-external-idp-with-wso2-api-manager-3-1-0-7f7a3a637526

https://medium.com/wso2-learning/understanding-wso2-api-manager-3rd-party-key-manager-integration-77a3677b1e9a

https://apim.docs.wso2.com/en/latest/administer/key-managers/configure-keycloak-connector/
