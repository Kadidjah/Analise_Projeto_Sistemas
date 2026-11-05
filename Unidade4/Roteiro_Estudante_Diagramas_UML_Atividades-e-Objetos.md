# Roteiro do estudante — Diagramas UML de Atividades e de Objetos

**Disciplina:** Análise e Projeto de Sistemas (APS)  
**Profa. Kadidja Valéria | APS**  
**Modalidade:** Atividade prática em grupo  
**Produto:** Dois diagramas UML documentados e versionados no GitHub

## 1. Objetivo da atividade

Cada grupo produzirá dois artefatos técnicos do próprio projeto APS: um **Diagrama de Atividades** e um **Diagrama de Objetos**. Ambos devem corresponder aos requisitos levantados e ser publicados no repositório GitHub do projeto.

## 2. Competências esperadas

- Traduzir requisitos em ações, decisões e caminhos alternativos.
- Representar objetos concretos, atributos, valores e links.
- Validar coerência entre requisitos, modelo de classes e diagramas.
- Documentar, versionar e publicar artefatos técnicos no GitHub.

## 3. Preparação — 15 minutos

- Recupere a ficha de requisitos da Aula 02 e o Diagrama de Classes, se já disponível.
- Escolha uma funcionalidade com início, fim e pelo menos uma decisão.
- Selecione uma situação concreta com pelo menos três objetos relacionados.
- Registre nomes dos integrantes, sistema e requisitos escolhidos.

## 4. Parte A — Diagrama de Atividades

1. **Defina o processo.** Exemplo: realizar empréstimo de livro.
2. **Liste as ações do fluxo principal** na ordem em que ocorrem.
3. **Identifique as decisões** e escreva as condições de guarda entre colchetes, como `[livro disponível]` e `[livro indisponível]`.
4. **Desenhe os elementos UML:** nó inicial, ações, fluxos de controle, decisões, mesclagens e nó final.
5. **Represente o paralelismo**, quando existir, com nós de bifurcação (*fork*) e sincronização (*join*).
6. **Use raias** (*swimlanes*) quando for importante distinguir os responsáveis pelas ações.
7. **Valide pelo menos dois cenários:** um fluxo de sucesso e um fluxo alternativo ou de falha.

**Exemplo — empréstimo de livro:**

```text
Início
  ↓
Identificar aluno
  ↓
Consultar disponibilidade
  ↓
Livro disponível?
  ├── [sim] → Registrar empréstimo → Atualizar estoque → Fim
  └── [não] → Informar indisponibilidade → Fim
```

> O fluxo textual acima é um **rascunho de análise**, não substitui a notação gráfica UML que deve ser entregue.

## 5. Parte B — Diagrama de Objetos

1. **Descreva o cenário em uma frase.** Exemplo: uma aluna possui um empréstimo ativo de um livro.
2. **Escolha as classes** necessárias para representar a situação.
3. **Crie instâncias nomeadas**, por exemplo, `aluno01 : Aluno`.
4. **Preencha atributos com valores concretos** coerentes com o cenário.
5. **Desenhe os links** entre as instâncias, respeitando as associações previstas no Diagrama de Classes.
6. **Revise a consistência** dos valores, relacionamentos e da situação representada.

**Exemplo — cenário de biblioteca:**

| Objeto (instância : Classe) | Atributos e valores de exemplo |
|---|---|
| `aluno01 : Aluno` | `nome = "Ana"`; `matricula = "2026001"` |
| `livro01 : Livro` | `titulo = "Engenharia de Software"`; `disponivel = false` |
| `emprestimo01 : Emprestimo` | `dataEmprestimo = "2026-11-05"`; `status = "ativo"` |

No diagrama, represente os três objetos em **retângulos UML com o nome da instância e da classe sublinhado**, seus atributos e os links `aluno01 — emprestimo01` e `emprestimo01 — livro01`, desde que essas relações existam no modelo de classes.

## 6. Ferramentas recomendadas

- [diagrams.net (draw.io)](https://app.diagrams.net/)
- [PlantUML](https://plantuml.com/)
- [Visual Paradigm Online](https://online.visual-paradigm.com/)
- [GitHub](https://github.com/)

## 7. Checklist antes da entrega

- [ ] O Diagrama de Atividades apresenta início, ações, decisões com guardas e fim.
- [ ] Os caminhos alternativos foram testados.
- [ ] O paralelismo, se presente, utiliza bifurcação e sincronização adequadas.
- [ ] O Diagrama de Objetos apresenta instâncias, atributos com valores e links.
- [ ] Os objetos são coerentes com o Diagrama de Classes.
- [ ] Ambos os diagramas são legíveis e correspondem aos requisitos do projeto.
- [ ] Os arquivos editáveis e as exportações em imagem ou PDF estão no GitHub.
- [ ] O `README.md` apresenta os cenários e os links para os diagramas.
- [ ] O commit possui mensagem descritiva.

## 8. Estrutura sugerida do repositório

```text
docs/
└── uml/
    ├── README.md
    ├── atividades/
    │   ├── diagrama-atividades-emprestimo.png
    │   └── diagrama-atividades-emprestimo.drawio
    └── objetos/
        ├── diagrama-objetos-emprestimo.png
        └── diagrama-objetos-emprestimo.drawio
```

> Os arquivos `.drawio` são exemplos para quem utiliza diagrams.net. Se a equipe usar outra ferramenta, mantenha seu formato-fonte editável.

## 9. Versionamento e entrega

Utilize nomes de arquivos em minúsculas, sem espaços e com hífens. Registre alterações por meio de commits com mensagens descritivas.

**Exemplo de mensagem de commit:**

```bash
git commit -m "docs(uml): adiciona diagramas de atividades e objetos do empréstimo"
```

No `README.md`, informe: objetivo dos diagramas, cenário representado, requisitos relacionados, ferramenta utilizada e links para os artefatos. Entregue o **link do repositório** e identifique o **commit da versão final**.

## 10. Critérios de avaliação sugeridos

| Critério | Peso sugerido |
|---|---:|
| Correção do Diagrama de Atividades | 30% |
| Correção do Diagrama de Objetos | 30% |
| Coerência com requisitos e classes | 20% |
| Documentação, organização e GitHub | 20% |
| **Total** | **100%** |

## 11. Entregáveis obrigatórios

1. Diagrama de Atividades do sistema do grupo.
2. Diagrama de Objetos de uma situação concreta do sistema.
3. Arquivos-fonte editáveis dos dois diagramas.
4. Exportações legíveis (PNG ou PDF).
5. `README.md` com descrição, cenários e rastreabilidade aos requisitos.
6. Link do repositório GitHub e identificação do commit final.

**Importante:** os diagramas fazem parte da **documentação técnica do projeto** e devem permanecer atualizados no GitHub sempre que houver alterações nos requisitos ou na modelagem.
