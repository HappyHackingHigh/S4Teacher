#
```
現代密碼

openssl
RSA非對稱式密碼實測(非對稱式密碼)
```
# openssl

https://zh.wikipedia.org/wiki/OpenSSL

https://www.openssl.org/ 

https://github.com/openssl/openssl

# XOR運算[python2]

https://en.wikipedia.org/wiki/XOR_cipher

```
>>> a=0b01010111011010010110101101101001
>>> k=0b11110011111100111111001111110011
>>> c=bin(a^k)
>>> print c
0b10100100100110101001100010011010
>>> d=bin(a^a^k)
>>> print d
0b11110011111100111111001111110011
```
```
作業:使用XOR運算時做兩整數互換

```
# openssl實測

# openssl help

```
Standard commands
asn1parse         ca                ciphers           cms               
crl               crl2pkcs7         dgst              dhparam           
dsa               dsaparam          ec                ecparam           
enc               engine            errstr            exit              
gendsa            genpkey           genrsa            help              
list              nseq              ocsp              passwd            
pkcs12            pkcs7             pkcs8             pkey              
pkeyparam         pkeyutl           prime             rand              
rehash            req               rsa               rsautl            
s_client          s_server          s_time            sess_id           
smime             speed             spkac             srp               
ts                verify            version           x509              

Message Digest commands (see the `dgst' command for more details)
blake2b512        blake2s256        gost              md4               
md5               rmd160            sha1              sha224            
sha256            sha384            sha512            

Cipher commands (see the `enc' command for more details)
aes-128-cbc       aes-128-ecb       aes-192-cbc       aes-192-ecb       
aes-256-cbc       aes-256-ecb       base64            bf                
bf-cbc            bf-cfb            bf-ecb            bf-ofb            
camellia-128-cbc  camellia-128-ecb  camellia-192-cbc  camellia-192-ecb  
camellia-256-cbc  camellia-256-ecb  cast              cast-cbc          
cast5-cbc         cast5-cfb         cast5-ecb         cast5-ofb         
des               des-cbc           des-cfb           des-ecb           
des-ede           des-ede-cbc       des-ede-cfb       des-ede-ofb       
des-ede3          des-ede3-cbc      des-ede3-cfb      des-ede3-ofb      
des-ofb           des3              desx              rc2               
rc2-40-cbc        rc2-64-cbc        rc2-cbc           rc2-cfb           
rc2-ecb           rc2-ofb           rc4               rc4-40            
seed              seed-cbc          seed-cfb          seed-ecb          
seed-ofb          
```



# 互動式 vs 指令式
先建立資料檔:
```
echo "123456789" > data.txt
echo "a123456789" > data2.txt
echo "A123456789" > data.txt
```
### 指令式
```
openssl sha1 data.txt
SHA1(data.txt)= 179c94cf45c6e383baf52621687305204cef16f9

openssl sha1 data2.txt
SHA1(data2.txt)= 02d707e871eb91f4a5dc34b6269d3469b987adbf

openssl sha1 data3.txt
SHA1(data3.txt)= 589a1c3dd871704c0e506a5b0386cffd932d9ef5
```
### 互動式
```
openssl
OpenSSL> sha1 datat.txt
datat.txt: No such file or directory
error in sha1
OpenSSL> sha1 data.txt
SHA1(data.txt)= 179c94cf45c6e383baf52621687305204cef16f9
OpenSSL> sha1 data1.txt 
data1.txt: No such file or directory
error in sha1
OpenSSL> sha1 data2.txt
SHA1(data2.txt)= 02d707e871eb91f4a5dc34b6269d3469b987adbf
OpenSSL> sha1 data3.txt
SHA1(data3.txt)= 589a1c3dd871704c0e506a5b0386cffd932d9ef5
OpenSSL> 

```

openssl enc -help
```
Usage: enc [options]
Valid options are:
 -help          Display this summary
 -ciphers       List ciphers
 -in infile     Input file
 -out outfile   Output file
 -pass val      Passphrase source
 -e             Encrypt
 -d             Decrypt
 -p             Print the iv/key
 -P             Print the iv/key and exit
 -v             Verbose output
 -nopad         Disable standard block padding
 -salt          Use salt in the KDF (default)
 -nosalt        Do not use salt in the KDF
 -debug         Print debug info
 -a             Base64 encode/decode, depending on encryption flag
 -base64        Same as option -a
 -A             Used with -[base64|a] to specify base64 buffer as a single line
 -bufsize val   Buffer size
 -k val         Passphrase
 -kfile infile  Read passphrase from file
 -K val         Raw key, in hex
 -S val         Salt, in hex
 -iv val        IV in hex
 -md val        Use specified digest to create a key from the passphrase
 -none          Don't encrypt
 -*             Any supported cipher
 -engine val    Use engine, possibly a hardware device
```

### 列出OpenSSL 提供的對稱式加解密演算法:openssl enc -ciphers

```
Supported ciphers:
-aes-128-cbc               -aes-128-cfb               -aes-128-cfb1             
-aes-128-cfb8              -aes-128-ctr               -aes-128-ecb              
-aes-128-ofb               -aes-192-cbc               -aes-192-cfb              
-aes-192-cfb1              -aes-192-cfb8              -aes-192-ctr              
-aes-192-ecb               -aes-192-ofb               -aes-256-cbc              
-aes-256-cfb               -aes-256-cfb1              -aes-256-cfb8             
-aes-256-ctr               -aes-256-ecb               -aes-256-ofb              
-aes128                    -aes128-wrap               -aes192                   
-aes192-wrap               -aes256                    -aes256-wrap              
-bf                        -bf-cbc                    -bf-cfb                   
-bf-ecb                    -bf-ofb                    -blowfish                 
-camellia-128-cbc          -camellia-128-cfb          -camellia-128-cfb1        
-camellia-128-cfb8         -camellia-128-ctr          -camellia-128-ecb         
-camellia-128-ofb          -camellia-192-cbc          -camellia-192-cfb         
-camellia-192-cfb1         -camellia-192-cfb8         -camellia-192-ctr         
-camellia-192-ecb          -camellia-192-ofb          -camellia-256-cbc         
-camellia-256-cfb          -camellia-256-cfb1         -camellia-256-cfb8        
-camellia-256-ctr          -camellia-256-ecb          -camellia-256-ofb         
-camellia128               -camellia192               -camellia256              
-cast                      -cast-cbc                  -cast5-cbc                
-cast5-cfb                 -cast5-ecb                 -cast5-ofb                
-chacha20                  -des                       -des-cbc                  
-des-cfb                   -des-cfb1                  -des-cfb8                 
-des-ecb                   -des-ede                   -des-ede-cbc              
-des-ede-cfb               -des-ede-ecb               -des-ede-ofb              
-des-ede3                  -des-ede3-cbc              -des-ede3-cfb             
-des-ede3-cfb1             -des-ede3-cfb8             -des-ede3-ecb             
-des-ede3-ofb              -des-ofb                   -des3                     
-des3-wrap                 -desx                      -desx-cbc                 
-id-aes128-wrap            -id-aes128-wrap-pad        -id-aes192-wrap           
-id-aes192-wrap-pad        -id-aes256-wrap            -id-aes256-wrap-pad       
-id-smime-alg-CMS3DESwrap  -rc2                       -rc2-128                  
-rc2-40                    -rc2-40-cbc                -rc2-64                   
-rc2-64-cbc                -rc2-cbc                   -rc2-cfb                  
-rc2-ecb                   -rc2-ofb                   -rc4                      
-rc4-40                    -seed                      -seed-cbc                 
-seed-cfb                  -seed-ecb                  -seed-ofb   
```
# DES對稱式密碼實測(對稱式密碼)
```
echo "a123456789" > infile

cat infile 
a123456789

加密
openssl des -in infile -out infile.des
enter des-cbc encryption password:
Verifying - enter des-cbc encryption password:

cat infile
a123456789

cat infile.des
��lted__���jd'2��g�
  ����
  
解密
openssl des -d -in infile.des -out sol
enter des-cbc decryption password:

cat sol
a123456789
```
# TRIPLE-DES對稱式密碼實測(對稱式密碼)[作業]
```
使用Triple DES加密openssl des3 -in file -out file.des3
使用Triple DES 解密openssl des3 -d -in file.des3 -out file
```
# RSA非對稱式密碼實測(非對稱式密碼)
```
genrsa
 
rsa 
  
rsautl
```
