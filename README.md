# CameraGuard

CameraGuard é um aplicativo leve para Windows voltado a gravação contínua de câmera e áudio, com foco em computadores modestos e cenários de longa duração.

## Estado atual

A versão **0.16.0 / R016.13** está em fase final de validação para a primeira release pública.

O núcleo atual inclui:

- gravação local resiliente com FFmpeg;
- perfil CFTV otimizado para baixo consumo;
- buffer local para continuar gravando mesmo quando a nuvem fica indisponível;
- arquivamento contínuo para uma pasta sincronizada;
- biblioteca e reprodução das gravações;
- diagnóstico de memória, encoder, armazenamento e fila de arquivamento;
- atualização segura pelo próprio aplicativo, usando manifesto assinado e verificação SHA-256;
- instalador Windows per-user, sem exigir privilégios administrativos.

## Downloads

A primeira versão pública será disponibilizada na seção **Releases** deste repositório.

> Enquanto a primeira release não estiver publicada, não há instalador oficial disponível neste repositório.

## Atualizações

O CameraGuard consulta o canal estável em:

`updates/stable.json`

Esse manifesto é assinado digitalmente e aponta para o instalador oficial publicado nas GitHub Releases.

## Armazenamento e segurança

A captura não depende diretamente da conexão com a internet. O CameraGuard grava primeiro em um spool local e arquiva arquivos já fechados para o destino em nuvem, mantendo uma margem local de segurança.

## Plataforma

- Windows 10/11 x64
- FFmpeg incluído no pacote de distribuição
- build self-contained do .NET

## Licença

Nenhuma licença open source foi concedida neste momento. O código e os binários permanecem sob os direitos do autor, salvo indicação diferente em uma release futura.

---

Desenvolvido por Hailton Reis.
