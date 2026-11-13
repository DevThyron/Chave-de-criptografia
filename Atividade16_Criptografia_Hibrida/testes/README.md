# Testes
# Roteiro de Testes — Criptografia Híbrida

## Teste 01 — Geração RSA
- Gerar chave privada RSA de 2048 bits.
- Extrair a chave pública.
- Resultado esperado: criação dos arquivos de chave.

## Teste 02 — Criptografia AES
- Criar uma mensagem de teste.
- Gerar um segredo aleatório.
- Criptografar a mensagem utilizando AES-256-CBC.
- Resultado esperado: geração do arquivo criptografado.

## Teste 03 — Proteção da chave AES
- Utilizar a chave pública RSA para proteger o segredo AES.
- Resultado esperado: geração do arquivo `chave_aes.enc`.

## Teste 04 — Descriptografia
- Recuperar o segredo AES utilizando a chave privada RSA.
- Descriptografar a mensagem.
- Resultado esperado: recuperar o conteúdo original.

## Teste 05 — Verificação SHA-256
- Calcular o hash SHA-256 da mensagem original.
- Calcular o hash SHA-256 da mensagem recuperada.
- Resultado esperado: hashes iguais.

## Status
Os testes serão marcados como concluídos após a execução e verificação de cada etapa.
