# CameraGuard — critérios de consolidação R13 RC1

**Estado: proposta em revisão. Não é uma autorização de release nem um manifesto de atualização.**

O canal oficial permanece na release pública `v0.16.0 / R016.13`. O procedimento documentado em `docs/RELEASE_PROCESS.md` exige **5/5 gates**, instalador validado, publicação do artefato, manifesto RSA assinado e verificação no atualizador. O repositório funciona como canal de distribuição; publicar a totalidade do código-fonte não é requisito.

## Evidência do ensaio R13

| Critério | Estado |
| --- | --- |
| .NET 8 / WPF compila e abre na máquina Windows | PASS na candidata R13 anterior |
| Biblioteca de gravações no Drive Desktop | 39 dias encontrados por leitura de manifestos |
| Player embutido na janela principal | PASS estrutural, sem homologação AV |
| Gravações originais preservadas e câmeras desativadas | Ensaio isolado |
| Capturas WPF e hashes | 10 imagens privadas verificadas na candidata anterior |
| Exportação A–B real de 5,5s, recibo SHA-256, decodificação completa | **HOLD** |
| Sincronia perceptiva de áudio e vídeo | **PENDENTE** |
| Proporção/layout após o player e em janela compacta | **PENDENTE** |
| Five production gates, instalação limpa e rollback | **PENDENTE** |

## Candidata R13 RC1

Preparada na área de staging do projeto, **não publicada como release**. Contém encerramento explícito de MediaElement, verificação antecipada do intervalo de exportação (0,2–120 s), espera pelo término da auditoria A–B antes de avaliar o resultado e screenshot da volta ao painel após fechar o player (em vez de redimensionar a janela visível para capturar o modo compacto). Foram realizadas **167 verificações estáticas**, sem compilação Windows desta revisão.

## Bloqueios para uma nova versão pública

1. Construir a R13 RC1 no Windows com 0 erros e revisar proporção e comportamento do player, incluindo redimensionamento manual.
2. Validar mídia real por reprodução, áudio, seek, pausa, A–B de 5,5s e decodificação integral do arquivo gerado. Se os eventos registrarem falha ou timeout, permanecer em HOLD.
3. Confirmar SHA de origem antes/depois; testar leitura do Drive desconectado/reconectado e persistência das gravações.
4. Executar integralmente os **5/5 gates de produção**, incluindo gravação física e políticas críticas de backup, retenção e migração; não inferir sucesso por capturas estáticas.
5. Gerar e testar instalador limpo; verificar digest, tamanho, assinatura RSA do manifesto e capacidade de rollback.
6. Somente após aprovação explícita, publicar GitHub Release e atualizar o canal `updates/stable.json` pelo procedimento assinado. Nunca colocar chave privada de release no repositório ou Drive.

## Escopo posterior

Login OAuth do Google Drive, câmeras YouSee e visualização móvel são melhorias planejadas **após** a estabilização desta candidata. Não devem aumentar o risco da release atual.

Nenhum arquivo de mídia privada, credencial, base de dados ou log com caminhos locais integra esta proposta.