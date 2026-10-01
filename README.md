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

## Perfis de uso

O CameraGuard foi pensado como uma ferramenta de **proteção, registro e respaldo**, e não apenas como um gravador comum.

| Perfil | Exemplos de uso | Objetivo |
|---|---|---|
| **Pessoal** | casa, escritório particular, bancada, garagem | registrar eventos e aumentar a segurança do ambiente |
| **Educacional** | aula particular, sala de reforço, laboratório, atendimento supervisionado | documentar incidentes e dar respaldo a alunos, responsáveis e profissionais |
| **Profissional** | escritório, recepção, loja, restaurante, coworking | registrar situações relevantes em áreas autorizadas |
| **CFTV leve** | pequenos negócios, salas técnicas, postos de atendimento | gravação prolongada com baixo consumo e recuperação simples |

Em cenários educacionais, especialmente quando houver crianças, o CameraGuard deve ser utilizado com ciência dos responsáveis, finalidade definida, acesso restrito às gravações e respeito às regras de privacidade aplicáveis.

## Plataformas

| Plataforma | Estado |
|---|---|
| **Windows 10/11 x64** | ✅ **Disponível — v0.16.0** |
| **Windows ARM64** | 🧭 Em breve |
| **Linux (Flatpak)** | 🧭 Planejado |
| **macOS** | 🧭 Planejado |

A arquitetura futura pretende manter o núcleo de gravação e armazenamento compartilhado e adaptar a camada de captura às APIs nativas de cada sistema.

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

Recursos futuros que envolvam automação de vigilância, auditoria ou captura adicional de dados serão projetados com controles explícitos de ativação, transparência e privacidade.

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

## Roadmap

O CameraGuard continuará evoluindo além da primeira release pública. O roadmap atual é indicativo e pode mudar conforme testes e prioridades do projeto.

### Próximos passos

- **Modo de proteção ao bloquear a sessão do Windows**: iniciar ou manter a gravação quando o usuário usar `Win + L`, preservando o computador bloqueado enquanto o ambiente continua sendo monitorado.
- Refinamento do consumo de CPU, memória e armazenamento em gravações longas.
- Melhorias no histórico, recuperação e gerenciamento das gravações.
- Novos controles de privacidade e políticas para cenários corporativos.
- Melhorias de instalação, atualização e diagnóstico.

### Multiplataforma

Está planejada a expansão do CameraGuard para outros sistemas operacionais:

- **Windows ARM64** — planejado como uma futura build nativa, mantendo a base atual e adaptando dependências/binários nativos quando necessário.
- **Linux** — versão planejada com **Flatpak como formato principal de distribuição**, visando uma experiência consistente entre distribuições e futura publicação no Flathub. O backend de captura e as permissões de câmera/microfone/armazenamento precisarão ser adaptados ao ecossistema Linux.
- **macOS** — versão planejada, incluindo adaptação às APIs de captura, permissões de câmera/microfone e empacotamento do macOS.

A versão atual continua sendo **Windows x64**. Windows ARM64, Linux e macOS ainda não possuem builds públicas nem prazo de lançamento anunciado.

### Em estudo

Também estão sendo estudados novos recursos de segurança e auditoria para uso pessoal e corporativo. Funcionalidades que envolvam dados adicionais do usuário ou do ambiente somente serão promovidas a recursos públicos após avaliação técnica, de privacidade e de conformidade.

## Status do projeto

**v0.16.0 / R016.13 — primeira release pública estável.**

As próximas versões continuarão priorizando:

- baixo consumo;
- estabilidade em gravações longas;
- melhor experiência de vigilância;
- automação de proteção e recuperação;
- expansão multiplataforma;
- melhorias de usabilidade e privacidade.

## Licença

Nenhuma licença open source foi concedida neste momento.

O código-fonte, os binários, a identidade visual e os demais materiais permanecem sob os direitos do autor, salvo indicação diferente em uma versão futura.

---

Desenvolvido por **Hailton Reis**.
