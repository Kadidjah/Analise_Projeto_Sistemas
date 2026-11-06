# Bot Facul Resolve — especificação de implementação

**Objetivo:** orientar a criação do assistente conversacional do Facul Resolve na plataforma SERPROBot, usando a documentação de desenvolvimento como referência para configurar intenções, entidades, variáveis de conversa, respostas e integrações.

> **Importante:** este repositório ainda não contém código do sistema Facul Resolve nem uma API de ocorrências. Por isso, este artefato define o fluxo do bot e o contrato esperado com o backend, mas não inventa sintaxe de configuração do SERPROBot nem afirma que a integração já está publicada. Transfira os diálogos para os componentes/formato exatos descritos na documentação oficial e substitua os endpoints ilustrativos pelos endpoints reais da instituição.

## 1. Escopo do MVP

O bot ajuda estudantes e servidores a:

1. registrar um problema de infraestrutura ou serviço da instituição;
2. consultar o andamento de uma ocorrência pelo protocolo;
3. entender como e quais informações são necessárias para abrir um chamado;
4. pedir atendimento humano quando o bot não resolver a solicitação.

Exemplos de problemas: projetor, banheiro, iluminação, Wi-Fi, cadeira, ar-condicionado, bebedouro e computador.

## 2. Modelo conversacional

Configure no SERPROBot os equivalentes documentados de **intenções**, **entidades**, **variáveis/slots**, **respostas** e **ações**. Os nomes abaixo são identificadores sugeridos para o projeto, não uma afirmação sobre a sintaxe proprietária da plataforma.

### Intenções

| Identificador sugerido | Exemplos de fala | Resultado |
|---|---|---|
| `saudacao` | “Oi”, “Olá”, “Bom dia” | Apresentar opções principais |
| `registrar_problema` | “Quero reportar uma lâmpada queimada”, “Abrir chamado” | Iniciar coleta dos dados da ocorrência |
| `consultar_protocolo` | “Consultar meu chamado”, “Acompanhar ocorrência” | Solicitar ou reconhecer o protocolo |
| `informar_problema` | “O projetor não funciona” | Extrair/confirmar categoria e descrição durante o registro |
| `informar_local` | “Sala 203”, “Bloco B, banheiro do térreo” | Guardar o local informado |
| `informar_urgencia` | “Alta”, “É urgente”, “Pode esperar” | Guardar prioridade percebida; confirmar conforme regras institucionais |
| `ajuda` | “O que você faz?”, “Como funciona?” | Explicar os serviços do bot |
| `falar_com_pessoa` | “Atendente”, “Quero falar com alguém” | Informar canal humano oficial ou encaminhar, se integrado |
| `cancelar` | “Cancelar”, “Deixa pra lá” | Confirmar e encerrar o fluxo em andamento |
| `desconhecida` | Mensagem não reconhecida | Pedir reformulação e oferecer opções |

### Entidades sugeridas

- `categoria`: projetor, banheiro, iluminação, rede/Wi-Fi, mobiliário, climatização, bebedouro, computador, outro.
- `local`: sala, bloco, andar e/ou ponto de referência; aceitar texto livre.
- `urgencia`: alta, média ou baixa. Tratar como informação declarada pelo usuário, não como classificação automática definitiva.
- `protocolo`: identificador emitido pelo backend após registro.

### Variáveis da conversa

`fluxo_atual`, `categoria`, `descricao`, `local`, `urgencia`, `protocolo`, `consentimento_foto` (opcional) e `tentativas_reconhecimento`.

Não peça senha, documento pessoal, dados bancários ou informação sensível. Foto deve ser opcional; não solicite que a pessoa apareça nela. Se a plataforma não suportar upload de imagem seguro, explique que a foto não pode ser recebida pelo bot e permita continuar sem ela.

## 3. Fluxo: registrar problema

1. **Abertura:** “Vou ajudar a registrar um problema na instituição. Para começar, qual problema você encontrou?”
2. **Categoria:** reconhecer a categoria mencionada. Se não for possível, perguntar: “É sobre sala de aula, banheiro, iluminação, Wi-Fi, mobiliário, ar-condicionado, bebedouro, computador ou outro assunto?”
3. **Descrição:** pedir uma descrição objetiva. Se a primeira mensagem já descreveu o problema, confirmar em vez de perguntar novamente.
4. **Local:** “Onde acontece? Informe bloco, andar e sala ou um ponto de referência.” Se faltar precisão, pedir um complemento sem bloquear com campos impossíveis de fornecer.
5. **Urgência:** perguntar “Qual a urgência percebida: alta, média ou baixa?”. Informar que situações de risco imediato devem ser comunicadas também ao canal de emergência/segurança oficial da instituição; o bot não substitui esse canal.
6. **Resumo e confirmação:** mostrar categoria, descrição, local e urgência. Perguntar “Posso enviar?” com opções **Enviar**, **Corrigir** e **Cancelar**. Não registrar antes da confirmação explícita.
7. **Envio:** acionar a ação de backend `criar_ocorrencia` somente após validação e confirmação.
8. **Sucesso:** apresentar o protocolo retornado e instruir como consultar o andamento. Não inventar protocolo nem prometer prazo de solução.
9. **Falha:** manter os dados durante a sessão, informar que não foi possível enviar e oferecer nova tentativa ou canal oficial alternativo. Não afirmar que o chamado foi registrado sem resposta positiva do backend.

### Exemplo de conversa

```text
Bot: Olá! Sou o assistente do Facul Resolve. Posso registrar um problema ou consultar um protocolo. O que você precisa?
Pessoa: O projetor da sala 203 não funciona.
Bot: Entendi: problema no projetor. Qual bloco e andar ficam a sala 203?
Pessoa: Bloco A, segundo andar.
Bot: Como você considera a urgência: alta, média ou baixa?
Pessoa: Média.
Bot: Confira antes de enviar: projetor sem funcionamento; Bloco A, segundo andar, sala 203; urgência média. Posso registrar?
Pessoa: Sim.
Bot: Ocorrência registrada. Seu protocolo é [protocolo retornado pelo sistema]. Guarde-o para consultar o andamento.
```

## 4. Fluxo: consultar ocorrência

1. Solicitar o protocolo: “Informe o protocolo da ocorrência.”
2. Validar o formato no backend (não rejeitar por uma regra local não confirmada pela instituição).
3. Executar `consultar_ocorrencia`.
4. Se localizada, mostrar somente os campos autorizados: protocolo, status, data de atualização e mensagem pública da equipe responsável.
5. Se não encontrada, explicar que não foi localizada e pedir conferência do número; limitar tentativas e oferecer atendimento humano.
6. Se o serviço estiver indisponível, informar a indisponibilidade sem expor detalhes técnicos ou dados de outras pessoas.

## 5. Ações e contrato provisório do backend

Estas operações são **contratos conceituais**, não endpoints existentes. A equipe deve alinhá-los à API real, autenticação, autorização, política de retenção e modelo de dados da instituição.

### `criar_ocorrencia`

Entrada mínima sugerida: `categoria`, `descricao`, `local`, `urgencia` e identificador de sessão necessário à integração. A chamada só ocorre depois da confirmação do usuário.

Resposta esperada de sucesso: `protocolo` e, opcionalmente, uma mensagem/status inicial público. O bot deve usar o protocolo retornado pelo serviço.

### `consultar_ocorrencia`

Entrada: `protocolo` e credenciais/contexto de autorização exigidos pelo backend. Saída limitada ao status e às informações que o solicitante tem direito de consultar.

### Tratamento de erros

- `400`: pedir correção dos campos indicados sem revelar detalhes internos.
- `401/403`: não prosseguir; orientar a autenticação/canal institucional oficial.
- `404`: dizer que o protocolo não foi localizado.
- `429`: pedir que aguarde antes de tentar novamente.
- `5xx`/timeout: comunicar indisponibilidade e oferecer canal alternativo.

Nunca incluir tokens, segredos, stack traces ou dados pessoais nos textos enviados ao usuário ou nos logs de conversa.

## 6. Regras de interação e privacidade

- Usar português claro, acolhedor e frases curtas; oferecer opções quando houver dúvida.
- Fazer uma pergunta por vez e permitir corrigir ou cancelar em qualquer etapa.
- Pedir apenas dados necessários para encaminhar e localizar o problema.
- Informar, antes da coleta, para que os dados serão usados e apontar o aviso de privacidade institucional aplicável.
- Coletar consentimento específico antes de qualquer dado opcional, como foto ou contato adicional.
- Aplicar controles de acesso, retenção mínima, proteção contra abuso e sanitização definidos pelo backend e pela instituição (incluindo avaliação de LGPD).
- Não expor conteúdo privado de chamados em canais compartilhados; autenticação/identificação deve ser responsabilidade do serviço oficial.
- Não simular atendimento humano, confirmação de registro ou prazo de resolução.
- Disponibilizar canal alternativo real, configurado pela instituição, para falhas, urgências e solicitações fora do escopo.

## 7. Critérios de aceite

1. Uma pessoa consegue iniciar um registro com linguagem natural e o bot coleta categoria, descrição, local e urgência.
2. O bot apresenta um resumo e só chama a criação após confirmação explícita.
3. Um envio bem-sucedido apresenta exatamente o protocolo recebido do backend.
4. Uma falha de envio não é apresentada como sucesso e oferece alternativa adequada.
5. A consulta apresenta somente o status retornado para o protocolo informado e autorizado.
6. Mensagem não reconhecida, cancelamento e correção têm respostas previsíveis e não descartam dados sem aviso.
7. Nenhum fluxo solicita senha ou informação sensível desnecessária.
8. Foto é opcional e não impede o registro quando ausente.

## 8. Casos de teste conversacionais

| Caso | Entrada/condição | Resultado esperado |
|---|---|---|
| Registro completo | Problema, local, urgência e confirmação | Ação de criação chamada uma vez; protocolo exibido |
| Confirmação negativa | Usuário escolhe cancelar no resumo | Nenhuma ocorrência criada; conversa encerrada com confirmação |
| Dados incompletos | Descrição sem local | Bot pergunta o local, sem enviar ainda |
| Correção | Usuário corrige sala no resumo | Resumo atualizado antes do envio |
| Erro de backend | Serviço indisponível | Mensagem honesta, sem protocolo fictício, com canal alternativo |
| Protocolo inexistente | Consulta retorna não encontrado | Orientar conferência e oferecer ajuda |
| Fora do escopo | Pedido não relacionado ao sistema | Explicar escopo e oferecer opções/canal humano |
| Risco imediato | Pessoa relata perigo | Orientar canal oficial de emergência/segurança e não depender do registro comum |

## 9. Publicação no SERPROBot

1. Criar/configurar o bot no ambiente de desenvolvimento previsto pela documentação oficial do SERPROBot.
2. Definir intents, entidades, variáveis e transições equivalentes às deste documento usando o formato efetivamente documentado pela plataforma.
3. Cadastrar mensagens de fallback, cancelamento, confirmação e erro.
4. Implementar ações de integração no ambiente de execução suportado pela plataforma, mantendo segredos fora do fluxo e do repositório.
5. Configurar a URL real do backend, autenticação, timeout e tratamento dos códigos de resposta.
6. Executar os casos de teste acima em ambiente de homologação e validar os textos e a política de dados com a instituição.
7. Publicar somente após existir canal humano e aviso de privacidade reais, além da aprovação do responsável pelo sistema.

**Dependências para uma integração executável:** documentação/configuração específica da instância SERPROBot usada, API do Facul Resolve, método de autenticação, URL do canal humano oficial e regras de privacidade/retenção da instituição.
