# CameraGuard

Aplicativo leve de vigilância para Windows, voltado a **gravação contínua de câmera e microfone** com foco em baixo consumo de recursos, estabilidade e operação prolongada.

[![Latest Release](https://img.shields.io/github/v/release/Hailton-Reis/CameraGuard?label=release)](https://github.com/Hailton-Reis/CameraGuard/releases/latest)
![Windows](https://img.shields.io/badge/Windows-10%20%7C%2011-0078D4?logo=windows)
![Architecture](https://img.shields.io/badge/arch-x64-informational)

## Download

A versão pública atual é **CameraGuard v0.16.0 — R016.13**.

**[Baixar a versão mais recente](https://github.com/Hailton-Reis/CameraGuard/releases/latest)**

Instalador oficial:

```text
CameraGuard-Setup-0.16.0-win-x64.exe
```

SHA-256 da v0.16.0:

```text
a18e0476abb98e8412b584b30d9ff7d8b750d9cd7eb125d0c74571fdc80faad7
```

> O instalador atual ainda não possui assinatura Authenticode. Por isso, o Windows SmartScreen pode exibir um aviso em alguns computadores. Sempre baixe o CameraGuard pela página oficial de Releases deste repositório.

## O que é o CameraGuard?

O CameraGuard transforma uma webcam e um microfone conectados ao computador em um sistema simples de gravação contínua.

O projeto foi pensado principalmente para cenários como:

- monitoramento prolongado de um ambiente;
- uso em notebooks e computadores modestos;
- gravação com baixo consumo de CPU, memória e armazenamento;
- proteção contra perda de gravações quando a internet ou a pasta em nuvem fica temporariamente indisponível;
- consulta posterior das gravações pelo próprio aplicativo.

## Principais recursos

- **Gravação contínua de vídeo e áudio**
- **Perfil CFTV otimizado para baixo consumo**
- Resolução de vigilância em **720p**, com controle adaptativo de quadros
- Uso de **aceleração por hardware quando disponível**, com fallback automático
- **FFmpeg incluído** no pacote de distribuição
- Buffer local para proteger a gravação contra falhas de internet ou sincronização
- Arquivamento contínuo para uma pasta configurável
- Compatível com pastas sincronizadas por serviços como Google Drive Desktop
- Histórico integrado de gravações
- Reprodução de arquivos locais e arquivados
- Diagnóstico de câmera, microfone, encoder, memória, armazenamento e fila de arquivamento
- Preflight antes da gravação
- Inicialização opcional com o Windows
- Prevenção de suspensão durante a gravação
- Atualizador integrado via **GitHub Releases**
- Instalador por usuário, sem necessidade de privilégios administrativos

## Como funciona o armazenamento

O CameraGuard evita gravar diretamente em uma pasta de nuvem durante a captura.

A arquitetura utilizada é:

```text
Câmera + Microfone
        ↓
      FFmpeg
        ↓
   Buffer local
        ↓
arquivo fechado e validado
        ↓
Pasta de arquivamento / nuvem
```

Isso mantém a gravação funcionando mesmo quando a internet ou o cliente de sincronização apresenta lentidão ou indisponibilidade temporária.

Arquivos já fechados são transferidos para o destino configurado, enquanto o buffer local funciona como margem de segurança.

## Atualizações

O CameraGuard verifica atualizações diretamente na API de **GitHub Releases** deste repositório.

O fluxo é simples:

```text
CameraGuard instalado
        ↓
GitHub Releases / latest
        ↓
compara a versão publicada
        ↓
nova versão disponível?
        ↓
oferece download ao usuário
        ↓
valida tamanho + SHA-256
        ↓
instala após confirmação
```

O aplicativo procura pelo asset no padrão:

```text
CameraGuard-Setup-<versão>-win-x64.exe
```

Não é necessário `stable.json`, chave privada ou servidor próprio de atualização.

## Instalação

1. Acesse **[Releases](https://github.com/Hailton-Reis/CameraGuard/releases/latest)**.
2. Baixe o arquivo `CameraGuard-Setup-<versão>-win-x64.exe`.
3. Execute o instalador.
4. Abra o CameraGuard.
5. Em **Configurações**, selecione a câmera, o microfone e o local de armazenamento desejado.
6. Execute o **preflight** para conferir os dispositivos.
7. Inicie a gravação.

O aplicativo é instalado em:

```text
%LOCALAPPDATA%\Programs\CameraGuard
```

As configurações e os dados internos do usuário ficam separados em:

```text
%LOCALAPPDATA%\CameraGuard
```

A desinstalação preserva os dados do usuário e não remove automaticamente as gravações.

## Requisitos

- Windows 10 ou Windows 11
- Arquitetura x64
- Webcam compatível com Windows / DirectShow
- Microfone compatível com Windows / DirectShow
- Espaço livre em disco para o buffer e as gravações

O pacote é **self-contained**: não é necessário instalar o .NET separadamente.

## Validação da v0.16.0

A release **0.16.0 / R016.13** passou pela validação completa do projeto antes da publicação:

| Verificação | Resultado |
|---|---|
| Build | 0 warnings / 0 errors |
| Publish self-contained | PASS |
| Smoke HLS/fMP4 | PASS |
| Interface e configurações | PASS |
| Preflight | PASS |
| Gravação física | PASS |
| Diagnóstico durante gravação | PASS |
| Encerramento limpo | PASS |
| FFmpeg órfão após saída | 0 |
| Eventos relevantes de crash | 0 |

## Privacidade

O CameraGuard foi desenvolvido para executar a captura localmente no computador.

O usuário é responsável por configurar o ambiente, o destino das gravações e por utilizar câmera e microfone de acordo com as leis, políticas internas e regras de privacidade aplicáveis ao local onde o programa estiver sendo usado.

## Segurança do download

Para reduzir o risco de arquivos incorretos ou corrompidos:

- baixe o instalador somente pelas **Releases oficiais** deste repositório;
- o atualizador aceita somente o asset esperado para a versão publicada;
- o tamanho e o **SHA-256 fornecidos pelo GitHub** são verificados antes da instalação de uma atualização.

## Desenvolvimento

O projeto utiliza principalmente:

- C# / .NET 8
- Windows Forms
- FFmpeg
- DirectShow
- Inno Setup
- GitHub Releases para distribuição e atualização

## Status do projeto

**v0.16.0 / R016.13 — primeira release pública estável.**

Próximas versões continuarão priorizando:

- baixo consumo;
- estabilidade em gravações longas;
- melhor experiência de vigilância;
- automação de proteção e recuperação;
- melhorias de usabilidade.

## Licença

Nenhuma licença open source foi concedida neste momento.

O código-fonte, os binários, a identidade visual e os demais materiais permanecem sob os direitos do autor, salvo indicação diferente em uma versão futura.

---

Desenvolvido por **Hailton Reis**.
