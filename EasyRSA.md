
1. # Descarregar script EasyRSA https://github.com/OpenVPN/easy-rsa/releases:
   `wget https://github.com/OpenVPN/easy-rsa/releases/download/v3.1.7/EasyRSA-3.1.7.tgz`
   # ou com a CA já criada » (recomendado em aula)
   `wget https://github.com/luisfrazao/frazao/blob/master/EasyRSA-3.1.7--SS.zip`

2. # descompactar e alterar o email no ficheiro vars (email igual ao configurado no Thunderbird):
   # comandos em Bash
   
tar -xvzf EasyRSA-3.1.7.tgz        ou      unzip EasyRSA-3.1.7--SS.zip
cd EasyRSA-3.1.7

cp vars.example vars

vim vars
	set_var EASYRSA_DN      "org"
	set_var EASYRSA_REQ_COUNTRY     "PT"  
	set_var EASYRSA_REQ_PROVINCE    "Leiria"  
	set_var EASYRSA_REQ_CITY        "Leiria"  
	set_var EASYRSA_REQ_ORG "IPLeiria"  
	set_var EASYRSA_REQ_EMAIL       "xxxx@ipleiria.pt"  
	set_var EASYRSA_REQ_OU          "Segurança de Sistemas"


3. # se usou o ZIP não precisa de realizar este dois comandos. 
./easyrsa init-pki
./easyrsa build-ca
--------

4. # criar o seu certificado, substituindo "oMeuNome"
./easyrsa gen-req oMeuNome nopass
./easyrsa sign-req email oMeuNome
# pass para assinar é: "1234"

cd pki
./easyrsa export-p12 oMeuNome
# ou em openssl 
openssl pkcs12 -export -in issued/oMeuNome.crt -inkey private/oMeuNome.key -out oMeuNome_merged.p12

# importar o ficheiro para o thunderbird.
