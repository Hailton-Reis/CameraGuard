# Processo de release

## CameraGuard 0.16.0 / R016.13

O fluxo oficial de publicação é:

1. Executar `00_BUILD_E_VALIDAR.cmd`.
2. Confirmar **5/5 Gates PASS**.
3. Executar `02_GERAR_INSTALADOR.cmd`.
4. Testar o instalador gerado em uma instalação limpa.
5. Criar a GitHub Release com tag `v0.16.0`.
6. Anexar `CameraGuard-Setup-0.16.0-win-x64.exe`.
7. Executar `04_PREPARAR_RELEASE_GITHUB.cmd` no projeto de desenvolvimento.
8. Publicar o `stable.json` gerado em `updates/stable.json`.
9. Validar no aplicativo o fluxo **Verificar → Baixar → Instalar atualização**.
10. Concluir o teste de perda de internet/Drive e recuperação automática antes de marcar a release como final.

## Segurança do updater

O manifesto de atualização é assinado com RSA. O aplicativo contém somente a chave pública.

A chave privada deve permanecer fora:
- deste repositório;
- do Google Drive do projeto;
- do instalador;
- do diretório publicado do aplicativo.

O instalador também é validado por tamanho e SHA-256 antes da aplicação.

## Código-fonte

Este repositório está sendo usado inicialmente como canal oficial de distribuição e documentação. A publicação do código-fonte não é necessária para distribuir o instalador.
