Introdução à Análise e Projeto de Sistemas de Informação.
Conceitos e elementos fundamentais da engenharia de software - definição, características e tipos de
modelagens. Ferramentas Case de apoio ao desenho dos diagramas UML


# Ficha de Requisitos — Aula 02

## Análise e Projeto de Sistemas

**Unidade:** II — Introdução à Análise e Projeto de Sistemas  
**Atividade:** Transformação do levantamento do sistema em requisitos funcionais e não funcionais  
**Objetivo:** Registrar, de forma estruturada, o que o sistema deve fazer e quais características de qualidade deve atender.

---

## 1. Identificação do Sistema

| Campo | Preenchimento |
|---|---|
| Nome do sistema | Sistema de Biblioteca |
| Objetivo | Gerenciar cadastro de usuários, livros, empréstimos, devoluções e multas. |
| Público-alvo | Alunos, bibliotecários e administradores. |
| Responsável pelo levantamento | Grupo de estudantes |
| Versão | 1.0 |

---

# 2. Requisitos Funcionais

> Requisitos funcionais descrevem **funcionalidades ou serviços que o sistema deve oferecer**.

## RF01 — Cadastrar usuário

| Campo | Descrição |
|---|---|
| **Identificação** | RF01 |
| **Descrição** | O sistema deve permitir que o bibliotecário cadastre usuários da biblioteca. |
| **Prioridade** | Alta |
| **Critérios de aceitação** | 1. Deve permitir informar nome, matrícula, e-mail e telefone. 2. Deve impedir cadastro sem nome e matrícula. 3. Deve informar ao usuário quando o cadastro for concluído. |
| **Exemplo** | O bibliotecário informa os dados de um aluno e seleciona **Cadastrar**. O sistema valida os dados e registra o novo usuário. |

## RF02 — Cadastrar livro

| Campo | Descrição |
|---|---|
| **Identificação** | RF02 |
| **Descrição** | O sistema deve permitir cadastrar livros disponíveis na biblioteca. |
| **Prioridade** | Alta |
| **Critérios de aceitação** | 1. Deve permitir informar título, autor, ISBN e quantidade disponível. 2. Deve impedir o cadastro de livro sem título. 3. Deve apresentar confirmação após o cadastro. |
| **Exemplo** | O bibliotecário cadastra o livro *Engenharia de Software*, informa autor e ISBN, e o sistema registra o exemplar. |

## RF03 — Realizar empréstimo

| Campo | Descrição |
|---|---|
| **Identificação** | RF03 |
| **Descrição** | O sistema deve permitir registrar o empréstimo de um livro para um usuário habilitado. |
| **Prioridade** | Alta |
| **Critérios de aceitação** | 1. Deve verificar se o usuário está cadastrado. 2. Deve verificar a disponibilidade do livro. 3. Deve registrar usuário, livro, data do empréstimo e data prevista para devolução. 4. Deve atualizar a quantidade disponível. |
| **Exemplo** | O bibliotecário seleciona o aluno e o livro. O sistema verifica a disponibilidade e registra o empréstimo. |

## RF04 — Registrar devolução

| Campo | Descrição |
|---|---|
| **Identificação** | RF04 |
| **Descrição** | O sistema deve permitir registrar a devolução de um livro emprestado. |
| **Prioridade** | Alta |
| **Critérios de aceitação** | 1. Deve localizar o empréstimo. 2. Deve registrar a data de devolução. 3. Deve atualizar a disponibilidade do livro. 4. Deve verificar se houve atraso. |
| **Exemplo** | O bibliotecário registra a devolução. O sistema atualiza o estoque e verifica se o prazo foi cumprido. |

## RF05 — Calcular multa

| Campo | Descrição |
|---|---|
| **Identificação** | RF05 |
| **Descrição** | O sistema deve calcular a multa quando um livro for devolvido após o prazo estabelecido. |
| **Prioridade** | Média |
| **Critérios de aceitação** | 1. Deve comparar a data prevista com a data efetiva de devolução. 2. Deve calcular o valor conforme a regra definida pela biblioteca. 3. Deve registrar a multa vinculada ao usuário. |
| **Exemplo** | Um livro deveria ser devolvido em 10/09 e foi devolvido em 13/09. O sistema identifica o atraso e calcula a multa correspondente. |

## RF06 — Consultar disponibilidade de livro

| Campo | Descrição |
|---|---|
| **Identificação** | RF06 |
| **Descrição** | O sistema deve permitir consultar se determinado livro está disponível para empréstimo. |
| **Prioridade** | Média |
| **Critérios de aceitação** | 1. Deve permitir pesquisar por título, autor ou ISBN. 2. Deve informar a quantidade disponível. 3. Deve indicar quando não houver exemplares disponíveis. |
| **Exemplo** | O usuário pesquisa um livro pelo título e o sistema informa que existem dois exemplares disponíveis. |

---

# 3. Requisitos Não Funcionais

> Requisitos não funcionais descrevem **características, restrições e condições de qualidade** que o sistema deve atender.

## RNF01 — Segurança

| Campo | Descrição |
|---|---|
| **Identificação** | RNF01 |
| **Descrição** | O sistema deve controlar o acesso às funcionalidades conforme o perfil do usuário. |
| **Prioridade** | Alta |
| **Critérios de aceitação** | 1. Usuários devem autenticar-se antes de acessar funções restritas. 2. Funcionalidades administrativas devem estar disponíveis somente a perfis autorizados. |
| **Exemplo** | Um aluno não pode acessar a funcionalidade de cadastro de livros, disponível ao bibliotecário. |

## RNF02 — Usabilidade

| Campo | Descrição |
|---|---|
| **Identificação** | RNF02 |
| **Descrição** | A interface deve apresentar informações e comandos de forma clara e consistente. |
| **Prioridade** | Alta |
| **Critérios de aceitação** | 1. Os campos devem possuir rótulos claros. 2. Mensagens de erro devem orientar o usuário. 3. As ações principais devem ser facilmente identificáveis. |
| **Exemplo** | Ao deixar a matrícula vazia, o sistema informa que o campo é obrigatório. |

## RNF03 — Desempenho

| Campo | Descrição |
|---|---|
| **Identificação** | RNF03 |
| **Descrição** | Consultas comuns devem apresentar resposta em tempo adequado para o uso cotidiano. |
| **Prioridade** | Média |
| **Critérios de aceitação** | Em condições normais de operação, consultas simples devem apresentar o resultado em até 3 segundos. |
| **Exemplo** | Ao pesquisar um livro pelo título, o resultado deve ser apresentado em até 3 segundos. |

## RNF04 — Disponibilidade

| Campo | Descrição |
|---|---|
| **Identificação** | RNF04 |
| **Descrição** | O sistema deve estar disponível durante o horário de funcionamento da biblioteca. |
| **Prioridade** | Alta |
| **Critérios de aceitação** | O sistema deve permanecer acessível durante o período definido pela instituição, exceto em manutenções previamente programadas. |
| **Exemplo** | Durante o horário de atendimento, o bibliotecário consegue realizar empréstimos sem indisponibilidade não planejada. |

## RNF05 — Integridade dos dados

| Campo | Descrição |
|---|---|
| **Identificação** | RNF05 |
| **Descrição** | O sistema deve preservar a consistência dos dados registrados. |
| **Prioridade** | Alta |
| **Critérios de aceitação** | 1. Não deve permitir empréstimo de livro inexistente. 2. Não deve permitir quantidade de exemplares negativa. 3. Um empréstimo deve estar associado a usuário e livro válidos. |
| **Exemplo** | Ao tentar emprestar um livro sem exemplares disponíveis, o sistema bloqueia a operação e informa o motivo. |

---

# 4. Modelo para preenchimento pelos estudantes

## Requisito Funcional

| Campo | Resposta do grupo |
|---|---|
| Identificação | RF__ |
| Descrição | |
| Prioridade | Alta / Média / Baixa |
| Critérios de aceitação | |
| Exemplo | |

## Requisito Não Funcional

| Campo | Resposta do grupo |
|---|---|
| Identificação | RNF__ |
| Descrição | |
| Prioridade | Alta / Média / Baixa |
| Critérios de aceitação | |
| Exemplo | |

---

# 5. Orientações para elaboração

Para cada requisito, o grupo deve verificar:

- **Identificação:** possui código único?
- **Descrição:** está claro o que o sistema deve fazer ou qual característica deve apresentar?
- **Prioridade:** é essencial, importante ou pode ser implementado posteriormente?
- **Critérios de aceitação:** é possível verificar objetivamente se o requisito foi atendido?
- **Exemplo:** existe uma situação concreta que demonstra o requisito?

## Regra prática

Um bom requisito deve ser:

**Claro + específico + verificável + relevante**

---

# 6. Entregável da atividade

O grupo deverá entregar:

1. Identificação do sistema;
2. Pelo menos **5 requisitos funcionais**;
3. Pelo menos **3 requisitos não funcionais**;
4. Prioridade de cada requisito;
5. Critérios de aceitação;
6. Exemplo de utilização;
7. Identificação dos integrantes do grupo: (3 a 6 integrantes)

**Próxima etapa:** os requisitos produzidos nesta ficha servirão de base para a identificação e especificação dos **casos de uso**.
