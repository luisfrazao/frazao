

### 1. Descarregar script EasyRSA
   `wget https://github.com/OpenVPN/easy-rsa/releases/download/v3.1.7/EasyRSA-3.1.7.tgz`
   <br>
    **ou com a CA já criada » (recomendado em aula)**<br>
   `wget https://github.com/luisfrazao/frazao/raw/refs/heads/master/EasyRSA-3.1.7--SS.zip`

### 2. descompactar:
   ``` Bash
tar -xvzf EasyRSA-3.1.7.tgz        ou      unzip EasyRSA-3.1.7--SS.zip
cd EasyRSA-3.1.7
```
 não fazer o próximo comando se usarem  o unzip 
```
cp vars.example vars
```
editar o ficheiro vars e alterar o email (email igual ao configurado no Thunderbird)
```
vim vars
	set_var EASYRSA_DN      "org"
	set_var EASYRSA_REQ_COUNTRY     "PT"  
	set_var EASYRSA_REQ_PROVINCE    "Leiria"  
	set_var EASYRSA_REQ_CITY        "Leiria"  
	set_var EASYRSA_REQ_ORG "IPLeiria"  
	set_var EASYRSA_REQ_EMAIL       "xxxx@ipleiria.pt"  
	set_var EASYRSA_REQ_OU          "Segurança de Sistemas"
```

### 3. se usou o ZIP não precisa de realizar este dois comandos.
```
./easyrsa init-pki
./easyrsa build-ca
```
### 4. Criar o seu certificado, substituindo "oMeuNome"
```
./easyrsa gen-req oMeuNome nopass
./easyrsa sign-req email oMeuNome
»»»» pass para assinar é: "1234"

./easyrsa export-p12 oMeuNome
### ou com openssl: 
cd pki
openssl pkcs12 -export -in issued/oMeuNome.crt -inkey private/oMeuNome.key -out oMeuNome_merged.p12
```
### agora e' importar o ficheiro para o thunderbird.
