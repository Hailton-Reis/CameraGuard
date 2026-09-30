# Canal de atualização do CameraGuard

Esta pasta hospeda o manifesto público do canal **stable**.

O arquivo `stable.json` **não deve ser criado manualmente**. Ele é gerado pelo pipeline de release do projeto após:

1. o build passar pelos Gates de validação;
2. o instalador oficial ser gerado;
3. o artefato ser publicado na GitHub Release correspondente;
4. o manifesto ser assinado com a chave privada de release mantida fora do repositório.

O CameraGuard valida assinatura RSA, tamanho e SHA-256 antes de aceitar um pacote de atualização.

> A chave privada de assinatura nunca deve ser adicionada a este repositório.
