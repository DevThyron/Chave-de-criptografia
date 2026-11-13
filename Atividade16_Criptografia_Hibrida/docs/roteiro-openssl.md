# Roteiro de testes OpenSSL (simulação)

> Execute localmente. Não envie arquivos secretos ao GitHub.

## 1. Criar mensagem de teste
Crie `mensagem.txt` com um texto simples. (luiz e ivo vao fazer as deles diferentes

## 2. Gerar par RSA
```bash
openssl genpkey -algorithm RSA -out privada.pem -pkeyopt rsa_keygen_bits:2048
openssl pkey -in privada.pem -pubout -out publica.pem
```

## 3. Gerar material secreto aleatório
```bash
openssl rand -hex 32 > chave_aes.bin
```
O comando produz 32 bytes aleatórios codificados em hexadecimal (64 caracteres ASCII). Neste roteiro meio meme , esse valor é usado como segredo/senha de entrada do PBKDF2; não é passado como chave AES bruta.

## 4. Criptografar arquivo com AES-256-CBC + PBKDF2
```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -in mensagem.txt -out mensagem.enc -pass file:chave_aes.bin
```

## 5. Proteger o segredo com RSA-OAEP
```bash
openssl pkeyutl -encrypt -pubin -inkey publica.pem -in chave_aes.bin -out chave_aes.enc -pkeyopt rsa_padding_mode:oaep
```

## 6. Recuperar o segredo
```bash
openssl pkeyutl -decrypt -inkey privada.pem -in chave_aes.enc -out chave_aes_restaurada.bin -pkeyopt rsa_padding_mode:oaep
```

## 7. Restaurar a mensagem
```bash
openssl enc -d -aes-256-cbc -pbkdf2 -in mensagem.enc -out mensagem_restaurada.txt -pass file:chave_aes_restaurada.bin
```

## 8. Comparar hashes
```bash
openssl dgst -sha256 mensagem.txt
openssl dgst -sha256 mensagem_restaurada.txt
```
Os valores SHA-256 devem ser idênticos.

## 9. Assinatura digital (complemento)
```bash
openssl dgst -sha256 -sign privada.pem -out mensagem.sig mensagem.txt
openssl dgst -sha256 -verify publica.pem -signature mensagem.sig mensagem.txt
```
Resultado esperado da verificação: `Verified OK`.

## Observação importante
AES-CBC não autentica o conteúdo por si só. SHA-256 comparado após a restauração demonstra igualdade no teste, mas não substitui um mecanismo de autenticação criptográfica. Para um sistema real, prefira um modo autenticado como AES-GCM ou uma construção com MAC/assinatura.
