# SSL  
i'm going to genetate key_pair,  sign(hash the message{public_key + provided info}, then encrypt it with my private_key then send origenal message and encription to client),  
when it done by another well known CA's private_key that is known as cretificate.

## java Keytool  
**Create a folder _Keys_ open it in terminal**  
It comes with JRE.  
use to create own public/private key pairs and associated certificates for use in self-authentication.  
  
1. `keytool -genkey -alias Deb -keystore DebKeyStore.jks -keyalg RSA -sigalg SHA1withRSA`  
**genkey :** create key_pair  
**alias :**	short name of key_pair  
**keystore :** store key_pair into a file(jks it stores keys and certificate. this may hold many keys, it is password protected file.)  
**keyalg :** Key generation algorithm. RSA(mostly used)/ DSA(default)  
**sigalg :** signature algorithm. (make self-signed certificate)  
**SHA1withRSA :** hash the message(public_key, provided info) with SHA1, then encrypt it using a RSA private key.   
- Key Store Password >	password of the KeyStore.jks. (which is inside this KeyStore), by using this digist maked, 
so with out this no one can edit digist 
- provide info > Certificate owner's common name  
				Organization  
				Organizational unit  
				Locality or city  
				State or province  
				Country or region       
    				
2. `keytool -list -v -keystore DebKeyStore.jks`    
**list :** list all key_pair.    
**v :** human readable form (provided info).    
  
3. `keytool -list -protected -keystore DebKeyStore.jks`  
**protected :** now it wont ask (Key Store Password), but it only display key_paire names.   

4. `keytool -list  -rfc  -keystore DebKeyStore.jks`  
**rfc :** show all self-signed certificate (encrypted).    

#### export certificate(CER)  
5. `keytool -export -alias Deb -file Deb.cer -keystore DebKeyStore.jks`  
**export :** export that self-signed certificate.  
**file :** with in this file.  

6. `keytool -printcert -file Deb.cer`  
**printcert :** print certificate.  

#### create certificate signing request(CSR)   
CER won't work in browsers, we need well known CA's Cretificate. we need to make request.
7. `keytool -certreq -alias Deb -keystore DebKeyStore.jks -file Deb.csr`  
**certreq :** create csr.    

## Openssl  
**Create a folder _ open it in terminal**  
It comes with JRE.  
use to create own public/private key pairs and associated certificates for use in self-authentication.  


