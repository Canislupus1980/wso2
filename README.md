# wso2
for WSO2 Services (AM, IS, Analytics)

apt install openjdk-11-jre-headless

openssl pkcs12 -export -in domen.crt -inkey domen.key -name "*.domen.com" -certfile certificate_ca.crt -out domen.pfx

keytool -importkeystore -srckeystore domen.pfx -srcstoretype pkcs12 -destkeystore domen.jks -deststoretype JKS

ready certificates domain.jks put /home/wso2carbon/wso2am-4.1.0/repository/resources/security/

deployment.toml file - change the name to the desired certificate store
