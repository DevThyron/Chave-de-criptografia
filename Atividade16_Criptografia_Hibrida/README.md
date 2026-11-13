# Criptografia Híbrida — AES + RSA

Projeto acadêmico da disciplina **Segurança de Software**, do curso de Engenharia de Software (3º período) da UniRV.

## Grupo
- Thyron 
- Luiz 
- Ivo 

## Tecnologias
- Linguagem: C
- Interface: Terminal
- OpenSSL: biblioteca e ferramentas criptográficas

## Objetivo
Demonstrar criptografia híbrida: o conteúdo é protegido por criptografia simétrica AES e a chave de sessão é protegida por criptografia assimétrica RSA.

## Fluxo previsto
1. Selecionar/indicar um arquivo de entrada.
2. Gerar uma chave de sessão AES aleatória.
3. Criptografar o arquivo com AES-256-CBC, conforme o roteiro acadêmico.
4. Proteger a chave de sessão com a chave pública RSA do destinatário.
5. Recuperar a chave de sessão com a chave privada correspondente.
6. Descriptografar o arquivo.
7. Comparar SHA-256 do original e do arquivo restaurado.

## Estrutura
```text
Chave-de-criptografia/
├── README.md
├── .gitignore
├── src/
│   └── main.c
├── docs/
│   └── roteiro-openssl.md
├── evidencias/
│   └── README.md
└── testes/
    └── README.md
```

## Compilação
A implementação em C ainda deve ser adicionada. Quando `src/main.c` estiver implementado, a compilação poderá ser feita com um comando semelhante a:

```bash
gcc src/main.c -o criptografia -lcrypto
```

O comando exato dependerá das APIs OpenSSL utilizadas e da implementação final.

## Segurança
**Não publique** chaves privadas, chaves AES, senhas, arquivos criptografados de teste ou outros segredos. Os arquivos de evidência devem ocultar qualquer material secreto.

## Status
Checkpoint 1 — estrutura inicial e planejamento. A aplicação e o teste round-trip precisam ser implementados e comprovados pelo grupo.

## Disciplina
- Curso: Engenharia de Software — 3º período
- Instituição: UniRV — Universidade de Rio Verde
- Disciplina: Segurança de Software
- Professor: Vinícius Martinez de Oliveira
