# Facul Resolve — especificação acadêmica do bot

**Projeto:** Facul Resolve  
**Origem da proposta:** atividade “Dinâmica do Desenho” da Unidade 1, que propõe registrar problemas da instituição, informando tipo, local, descrição, foto opcional e urgência.  
**Tipo de solução:** assistente conversacional integrado ao sistema institucional de ocorrências.  
**Status:** proposta acadêmica; integração e publicação dependem da API institucional e da configuração real do SERPROBot.

## 1. Problema e objetivo

### Problema
Estudantes e servidores podem encontrar problemas de infraestrutura ou serviço e não ter um canal simples para informar o que aconteceu, indicar o local e acompanhar o encaminhamento. Relatos sem dados mínimos também podem dificultar a triagem.

### Objetivo
O Facul Resolve pretende facilitar, para estudantes e servidores, o registro e a consulta de problemas da instituição, contribuindo para encaminhamentos mais claros e rastreáveis.

## 2. Stakeholders

| Stakeholder | Papel e interesse |
|---|---|
| Estudante/servidor | Informar um problema e consultar seu andamento |
| Equipe responsável pela manutenção/serviço | Receber informações suficientes para avaliar e encaminhar ocorrências |
| Gestão da instituição | Acompanhar o processo e definir regras, canais e responsabilidades |
| Administrador do sistema | Configurar acessos, integrações, disponibilidade e segurança |
| Atendimento institucional | Ajudar em casos que o bot não resolve ou em indisponibilidade |

## 3. Requisitos funcionais

| ID | Requisito | Prioridade proposta |
|---|---|---|
| RF01 | O sistema deve permitir iniciar uma solicitação de registro por conversa. | Must |
| RF02 | O sistema deve coletar ou reconhecer categoria e descrição do problema, incluindo categorias como projetor, banheiro, iluminação, Wi-Fi, mobiliário, climatização, bebedouro e computador. | Must |
| RF03 | O sistema deve solicitar o local do problema, aceitando sala, bloco, andar ou ponto de referência. | Must |
| RF04 | O sistema deve permitir informar a urgência percebida como alta, média ou baixa. | Must |
| RF05 | O sistema deve apresentar um resumo e exigir confirmação explícita antes de enviar a ocorrência. | Must |
| RF06 | O sistema deve permitir corrigir os dados ou cancelar antes do envio. | Must |
| RF07 | Após resposta positiva do serviço institucional, o sistema deve apresentar o protocolo retornado pelo serviço. | Must |
| RF08 | O sistema deve permitir consultar o andamento a partir de um protocolo, mostrando apenas informações autorizadas. | Should |
| RF09 | O sistema deve oferecer ajuda e informar um canal institucional humano quando configurado. | Should |
| RF10 | O sistema pode permitir anexar foto opcional, caso a plataforma e a política institucional suportem o recebimento seguro. | Could |

## 4. Requisitos de qualidade

| ID | Requisito verificável proposto | Verificação |
|---|---|---|
| RQ01 — Desempenho | Em homologação, 95% das respostas que não dependem de integração devem ser exibidas em até 3 segundos. | Medir tempos em testes representativos. |
| RQ02 — Segurança e privacidade | O bot não deve solicitar senha ou dados pessoais não necessários e não deve expor segredos ou detalhes técnicos em respostas. | Revisão dos fluxos, testes e logs. |
| RQ03 — Usabilidade | Cada etapa deve fazer uma pergunta principal por vez e oferecer correção ou cancelamento antes do envio. | Teste de tarefa com usuários. |
| RQ04 — Confiabilidade | Em falha ou timeout do backend, o bot não deve confirmar registro nem gerar protocolo fictício. | Simular erros e verificar respostas. |
| RQ05 — Compatibilidade | Os fluxos devem ser testados nos canais e dispositivos oficialmente suportados pela instância SERPROBot. | Testes de homologação nos canais definidos. |

Os valores são metas propostas para validação com a instituição, não capacidades já medidas.

## 5. Regras de negócio propostas

| ID | Regra |
|---|---|
| RN01 | A ocorrência somente deve ser enviada após apresentação do resumo e confirmação explícita da pessoa. |
| RN02 | O protocolo deve ser criado e fornecido pelo sistema institucional; o bot não pode inventá-lo. |
| RN03 | A consulta deve respeitar as regras institucionais de autenticação e autorização e exibir somente dados permitidos. |
| RN04 | Foto é opcional; a ausência de foto não impede o registro. |
| RN05 | Em situação de risco imediato, o bot deve orientar o canal oficial de emergência/segurança e não se apresentar como substituto desse canal. |

As regras devem ser validadas pelos responsáveis da instituição antes da implantação.

## 6. Restrições e dependências

1. A publicação depende de uma API de ocorrências oficial com operações para criar e consultar solicitações.
2. A implantação deve usar os formatos, recursos de integração e configuração suportados pela instância SERPROBot indicada pela instituição e pela documentação oficial.
3. URL, autenticação, autorização, canal humano, aviso de privacidade e prazos de retenção ainda precisam ser definidos pelos responsáveis institucionais.
4. Nenhuma foto deve ser recebida até haver suporte seguro e aprovação da política institucional.

## 7. MoSCoW resumido

- **Must:** RF01–RF07, privacidade e tratamento honesto de falhas.
- **Should:** RF08 e RF09, após definir autenticação e canal oficial.
- **Could:** RF10, condicionado a suporte e política de imagens.
- **Won’t have nesta proposta:** classificação automática da gravidade, promessa de prazo de solução ou integração com serviços não fornecidos pela instituição.

## 8. Critérios de aceite

1. Dada uma descrição de problema, o bot coleta categoria, descrição, local e urgência, perguntando apenas os dados que faltam.
2. Antes de enviar, apresenta resumo e opções para confirmar, corrigir ou cancelar.
3. Sem confirmação explícita, nenhuma chamada de criação é realizada.
4. Em sucesso, apresenta o protocolo exato retornado pela API; em falha, não afirma que registrou.
5. A consulta não revela dados que a pessoa não esteja autorizada a acessar.
6. Foto não é obrigatória e nenhuma senha é solicitada.
7. Um relato de risco imediato recebe orientação para o canal institucional de emergência/segurança configurado.

## 9. Rastreabilidade com a atividade da Unidade 1

| Elemento do desenho da atividade | Requisito/fluxo correspondente |
|---|---|
| Tipo de problema | RF02 — categoria |
| Local (ex.: Sala 203) | RF03 — local |
| Descrição do problema | RF02 — descrição |
| Foto “Adicionar foto” | RF10 — anexo opcional |
| Urgência alta/média/baixa | RF04 — urgência percebida |
| Botão “Enviar problema” | RF05 — resumo e confirmação; RF07 — protocolo após sucesso |

## 10. Limites desta entrega

Este documento especifica uma proposta e não é um bot publicado ou conectado a serviços reais. A integração exige a API e as credenciais institucionais, configuração da instância SERPROBot, validação de privacidade e canal humano oficial. Os nomes de intenções e ações da especificação técnica são conceituais; a configuração final deve seguir a sintaxe efetivamente documentada para o ambiente utilizado.
