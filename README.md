![wso2](https://ticxar.co/wp-content/uploads/2019/12/apimngr.png)
# wso2
####for WSO2 Services (AM, IS, Analytics)####

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

![image](https://user-images.githubusercontent.com/86954730/222174542-3cf461ce-be36-4cc4-9cbd-278e1c6c605f.png)
