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

## Armazenamento e consumo estimado

O CameraGuard evita gravar diretamente em uma pasta de nuvem durante a captura. A gravação acontece primeiro em um **buffer local**, e somente arquivos já fechados e validados seguem para o destino de arquivamento.

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

Isso mantém a captura fora do caminho crítico da internet ou do cliente de sincronização. Se a nuvem ficar lenta ou temporariamente indisponível, o CameraGuard continua gravando localmente e tenta arquivar os arquivos depois.

### Quanto espaço a gravação ocupa?

No perfil CFTV atual, em um ensaio físico prolongado, foi observado consumo próximo de **0,355 GiB por hora**, aproximadamente **360 MB/h**.

A partir dessa taxa, uma referência prática é:

| Tempo de gravação contínua | Espaço aproximado |
|---|---:|
| 1 hora | ~0,36 GiB |
| 8 horas | ~2,8 GiB |
| 12 horas | ~4,3 GiB |
| 24 horas | ~8,5 GiB |
| 7 dias | ~60 GiB |
| 30 dias | ~256 GiB |

Uma estimativa aproximada de retenção, considerando o disco dedicado integralmente às gravações, seria:

| Capacidade nominal | Retenção aproximada |
|---|---:|
| 64 GB | ~7 dias |
| 128 GB | ~14 dias |
| 256 GB | ~28 dias |
| 512 GB | ~56 dias |
| 1 TB | ~109 dias |

> Esses números são **estimativas**, não limites fixos. O consumo real varia conforme quantidade de movimento na cena, câmera utilizada, encoder disponível, bitrate, áudio, perfil de qualidade e configurações avançadas.

Como referência adicional, **4 GiB de buffer local representam cerca de 11 horas de gravação** nessa taxa. O buffer funciona como margem de segurança antes do arquivamento para o destino configurado.

### Estratégia de armazenamento

O objetivo é manter três propriedades:

- **continuidade** — a gravação não depende da internet para continuar;
- **baixo I/O** — o CameraGuard evita usar a pasta de nuvem diretamente como destino ativo do FFmpeg;
- **recuperação** — arquivos já concluídos podem ser arquivados posteriormente quando o destino voltar a ficar disponível.

O destino pode ser uma pasta local, outro disco ou uma pasta sincronizada por serviços como Google Drive Desktop.

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
- **Linux** — versão planejada com **Flatpak como formato principal de distribuição**, visando uma experiência consistente entre distribuições e futura publicação no **Flathub**. Como opção secundária, também poderá existir uma build **AppImage** para uso portátil e instalação sem integração com loja. O backend de captura e as permissões de câmera/microfone/armazenamento precisarão ser adaptados ao ecossistema Linux.
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
