# wso2
for WSO2 Services (AM, IS, Analytics)

apt install openjdk-11-jre-headless

openssl pkcs12 -export -in domen.crt -inkey domen.key -name "*.domen.com" -certfile certificate_ca.crt -out domen.pfx

keytool -importkeystore -srckeystore domen.pfx -srcstoretype pkcs12 -destkeystore domen.jks -deststoretype JKS
