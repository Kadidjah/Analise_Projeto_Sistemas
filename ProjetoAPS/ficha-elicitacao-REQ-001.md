# Ficha de Elicitação de Requisitos

**Curso:** Engenharia de Software  
**Disciplina:** Análise e Projeto de Sistemas  
**Instituição:** UDF Centro Universitário  
**Grupo/integrantes:** ______________________________________________  
**Turma:** ____________________  **Data:** ____/____/______  **Versão:** 1.0

> Preencha uma ficha para cada requisito identificado. Registre a necessidade na linguagem do stakeholder e esclareça termos ambíguos antes de validar a ficha com ele.

## 1. Identificação do projeto

| Campo | Preenchimento |
|---|---|
| Nome do projeto | |
| Objetivo do projeto | Qual problema será resolvido e qual resultado se espera? |
| Contexto e escopo | Que processo ou serviço será contemplado? |

## 2. Stakeholder e fonte

| Campo | Preenchimento |
|---|---|
| Stakeholder (nome ou papel) | |
| Relação com o projeto | Usuário, cliente, gestor, especialista ou outro. |
| Contato ou setor (se aplicável) | |
| Técnica e data da elicitação | Entrevista, observação, questionário, oficina ou análise documental; data. |
| Responsável pelo registro | |

## 3. Requisito elicitado

| Campo | Preenchimento |
|---|---|
| ID do requisito | REQ-001 (numeração sequencial). |
| Necessidade relatada pelo stakeholder | Registre o que foi solicitado, de preferência com as palavras utilizadas na elicitação. |
| Descrição consolidada | O sistema deve... (ação observável, objeto e condições relevantes). |
| Justificativa ou benefício esperado | |
| Tipo | Funcional / qualidade / restrição. |
| Dependências ou dúvidas | |

## 4. Regras de negócio

| ID | Regra de negócio relacionada | Fonte ou responsável pela validação |
|---|---|---|
| RN-001 | | |
| RN-002 | | |

> Descreva políticas, condições e limites do domínio. Caso nenhuma regra tenha sido identificada, registre “Não identificada nesta etapa”.

## 5. Prioridade

**Classificação MoSCoW (marque uma):** [ ] Must have (essencial)  [ ] Should have (importante)  [ ] Could have (desejável)  [ ] Won't have nesta versão (fora do escopo atual)

**Justificativa da prioridade:** ______________________________________________

## 6. Critérios de aceitação

Escreva condições verificáveis que permitam decidir se o requisito foi atendido.

| ID | Dado/Quando | Então (resultado esperado) | Evidência ou forma de verificação |
|---|---|---|---|
| CA-01 | | | |
| CA-02 | | | |
| CA-03 | | | |

## 7. Validação e rastreabilidade

| Campo | Preenchimento |
|---|---|
| Situação | [ ] Pendente de validação  [ ] Validado  [ ] Necessita revisão |
| Validado por / data | |
| Observações e decisões | |
| Links relacionados | Issue, protótipo, caso de uso ou documento de origem. |

## Exemplo breve (fictício)

**Projeto:** Sistema de agendamento de atendimento acadêmico. **Objetivo:** permitir que estudantes reservem horários disponíveis. **Stakeholder:** estudante; entrevista em 24/09/2026. **REQ-001:** “Quero escolher um horário de atendimento pelo celular”. **Descrição:** O sistema deve permitir ao estudante autenticado reservar um horário disponível de atendimento. **RN-001:** um horário não pode receber mais de uma reserva ativa. **Prioridade:** Must have, pois a reserva é a função central. **CA-01:** dado um horário disponível, quando o estudante confirmar a reserva, então o sistema registra a reserva e retira o horário da lista de disponibilidade. **CA-02:** dado um horário já reservado, quando outro estudante tentar reservá-lo, então o sistema impede a duplicidade e apresenta uma mensagem clara.

## Como organizar no GitHub

1. No repositório do projeto, crie a pasta `docs/requisitos/`.
2. Salve esta ficha preenchida como `docs/requisitos/ficha-elicitacao-REQ-001.md`. Crie um arquivo por requisito, alterando o ID de forma sequencial. Guarde a versão PDF de cada ficha na mesma pasta, se a entrega também exigir PDF.
3. Pelo site do GitHub, use **Add file > Upload files** (ou crie/edite o Markdown com **Add file > Create new file**). Confirme os arquivos com uma mensagem de commit descritiva, como `docs: adiciona ficha de elicitação REQ-001`.
4. Atualize o `README.md` na raiz do repositório com uma seção de documentação e o link relativo:

```md
## Documentação de requisitos

- [Ficha de elicitação REQ-001](docs/requisitos/ficha-elicitacao-REQ-001.md)
- [Versão para impressão (PDF)](docs/requisitos/ficha-elicitacao-REQ-001.pdf)
```

5. Confira no GitHub se os links abrem e se o ID do arquivo coincide com o ID registrado na ficha. Atualize a ficha após validação, preservando o histórico de commits.
