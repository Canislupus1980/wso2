# wso2
for WSO2 Services (AM, IS, Analytics)

apt install openjdk-11-jre-headless

1. Get ready-made certificates

openssl pkcs12 -export -in domen.crt -inkey domen.key -name "*.domen.com" -certfile certificate_ca.crt -out domen.pfx

keytool -importkeystore -srckeystore domen.pfx -srcstoretype pkcs12 -destkeystore domen.jks -deststoretype JKS

2. Ready certificates domain.jks put /home/wso2carbon/wso2am-4.1.0/repository/resources/security/

3. deployment.toml file - change the name to the desired certificate store


[keystore.tls]
file_name =  "domen.jks"
type =  "JKS"
password =  "wso2carbon"
alias =  "*.domen.com"
key_password =  "wso2carbon"

![image](https://user-images.githubusercontent.com/86954730/222174542-3cf461ce-be36-4cc4-9cbd-278e1c6c605f.png)
