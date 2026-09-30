# CameraGuard v0.16.0 — R016.13

Primeira release pública candidata do CameraGuard.

## Destaques

- gravação contínua em Windows com FFmpeg;
- perfil CFTV leve para máquinas modestas;
- spool local resiliente, mantendo a captura fora do caminho crítico da nuvem;
- arquivamento contínuo para pasta sincronizada com staging atômico e SHA-256;
- recuperação automática de backlog;
- biblioteca e reprodução de gravações locais/nuvem;
- diagnóstico de RAM, encoder, armazenamento e fila;
- atualização segura pelo próprio aplicativo via manifesto RSA assinado;
- instalador per-user em `%LOCALAPPDATA%\Programs\CameraGuard`, sem exigir privilégios administrativos.

## Artefato oficial

**Arquivo:** `CameraGuard-Setup-0.16.0-win-x64.exe`  
**Tamanho:** 76.741.836 bytes  
**SHA-256:** `34def9577b7ccdcb4d21ff774892cb82074d090da97670d0b93bb285638ba0ca`

## Validação

O snapshot usado para o instalador passou:

- Gate 1 — prebuild / integridade: PASS
- Gate 2 — restore + build: PASS, 0 warnings / 0 errors
- Gate 3 — publish self-contained + FFmpeg + verify: PASS
- Gate 4 — verificação final da release: PASS
- Gate 5 — smoke HLS/fMP4: PASS, 12 fragments

No ensaio físico anterior, o caminho `FFmpeg -> spool local -> CloudArchiveService -> Google Drive Desktop` chegou a fila de aproximadamente 1 arquivo, sem retorno dos frame drops observados nas primeiras calibrações.

## Instalação

O instalador é per-user e não exige elevação administrativa. Configurações, catálogo, logs e gravações não ficam dentro da pasta do programa e não são removidos pela desinstalação.

## Atualizações

O aplicativo usa o canal:

`https://raw.githubusercontent.com/Hailton-Reis/CameraGuard/main/updates/stable.json`

O manifesto é validado por assinatura RSA e o instalador por tamanho + SHA-256.

## Observação sobre assinatura do Windows

Esta build ainda não possui certificado Authenticode público. O manifesto do updater é assinado, mas isso não substitui assinatura de código do Windows; portanto, o SmartScreen pode exibir aviso de publicador desconhecido.

## Checklist antes de marcar como FINAL

- instalação limpa do Setup;
- teste do aplicativo instalado;
- teste de perda de internet/Drive e drenagem no retorno;
- publicação do `updates/stable.json` assinado.
