# Ana — Assistente Virtual da Trama Store

Projeto desenvolvido para o desafio **["Construa Seu Assistente Virtual Com
Inteligência Artificial"](https://github.com/digitalinnovationone/dio-lab-bia-do-futuro)**
da [Digital Innovation One (DIO)](https://www.dio.me).

O desafio original usa como referência um agente de educação financeira
(["Edu"](https://github.com/falvojr/dio-lab-bia-do-futuro)). Este projeto
adapta a mesma proposta para outro contexto: **atendimento de uma loja de
moda**, aplicando os mesmos princípios de IA generativa e boas práticas de
UX estudados na trilha.

## O que este projeto entrega

Um protótipo de assistente virtual de atendimento (**Ana**) para uma loja
de roupas e calçados fictícia (**Trama Store**), capaz de:

- Responder **dúvidas frequentes (FAQ)** sobre trocas, devoluções, frete,
  pagamento, tamanhos, cuidados com as peças e disponibilidade em estoque.
- **Explicar produtos** do catálogo (tecido, cuidados, tamanhos, cores,
  preço).
- Fazer **simulações demonstrativas**: cálculo de parcelamento e
  conversão de tabela de tamanhos (BR → US → EU).
- **Manter o contexto da conversa**, respondendo perguntas de
  acompanhamento sobre o último produto mencionado sem que o nome precise
  ser repetido.
- **Admitir quando não sabe algo**, em vez de inventar uma resposta, e
  encaminhar para o atendimento humano.

O protótipo roda **100% offline e gratuitamente** — não depende de
nenhuma chave de API de IA generativa paga — usando busca por
palavras-chave sobre uma base de conhecimento local. A arquitetura já
prevê, de forma documentada, como evoluir para um LLM real (ver
[`docs/03-prompts.md`](docs/03-prompts.md)).

## Como rodar

Requer apenas Python 3.10+ (nenhuma dependência externa é obrigatória).

```bash
git clone <url-do-seu-fork>
cd assistente-virtual-moda
python src/app.py
```

Você verá a saudação da Ana e poderá conversar livremente pelo terminal.
Digite `sair` para encerrar. Alguns exemplos de mensagens para testar:

```
Qual o prazo de entrega?
Me fala sobre a camiseta essential
qual o preço dela?
simular parcelamento de 300 reais em 3 vezes
converter tamanho M para US
vocês vendem carros?
```

Uma conversa de exemplo completa (saída real da aplicação) está em
[`examples/conversa-exemplo.md`](examples/conversa-exemplo.md).

### Rodando a avaliação automática

```bash
python src/tests/test_app.py     # relatório de métricas no terminal
pytest src/tests/test_app.py -v  # como suíte de testes (opcional: pip install pytest)
```

## Estrutura do projeto

```
assistente-virtual-moda/
├── README.md                    # este arquivo
├── data/                        # base de conhecimento
│   ├── faq.json
│   ├── produtos.json
│   ├── perfil_cliente.json
│   └── historico_atendimento.csv
├── docs/                        # os 6 passos do desafio, documentados
│   ├── 01-documentacao-agente.md
│   ├── 02-base-conhecimento.md
│   ├── 03-prompts.md
│   ├── 04-metricas.md
│   └── 05-pitch.md
├── src/
│   ├── app.py                   # aplicação (lógica do agente + CLI)
│   └── tests/
│       └── test_app.py          # testes e relatório de avaliação
├── examples/
│   └── conversa-exemplo.md      # transcrição real de uma conversa
└── assets/                      # espaço reservado para imagens/vídeo do pitch
```

## Os 6 passos do desafio

| Passo | Onde está |
|---|---|
| 1. Documentação do agente | [`docs/01-documentacao-agente.md`](docs/01-documentacao-agente.md) |
| 2. Base de conhecimento | [`docs/02-base-conhecimento.md`](docs/02-base-conhecimento.md) |
| 3. Prompts do agente | [`docs/03-prompts.md`](docs/03-prompts.md) |
| 4. Aplicação funcional | [`src/app.py`](src/app.py) |
| 5. Avaliação e métricas | [`docs/04-metricas.md`](docs/04-metricas.md) |
| 6. Pitch | [`docs/05-pitch.md`](docs/05-pitch.md) |

## Decisões de projeto (por que assim?)

- **Tema (moda/varejo, não finanças)**: escolhido para mostrar que os
  mesmos princípios do desafio (base de conhecimento, honestidade sobre
  limites, contexto) se aplicam a qualquer domínio de atendimento, não
  apenas ao exemplo financeiro oficial.
- **Sem LLM externo por padrão**: garante que qualquer pessoa avaliando
  este repositório consiga rodar o projeto imediatamente, sem precisar de
  chave de API nem de instalar um modelo local. A lógica de decisão
  (`AssistenteModa` em `src/app.py`) foi escrita de forma que o *prompt*
  documentado em `docs/03-prompts.md` possa, no futuro, ser passado
  diretamente a um LLM real no lugar da busca por palavras-chave.
- **Dados fictícios**: todo o conteúdo em `data/` foi criado
  especificamente para este protótipo — nenhum dado real de clientes ou
  produtos foi utilizado.

## Créditos

- Desafio original: [Digital Innovation One](https://www.dio.me) —
  [repositório base](https://github.com/digitalinnovationone/dio-lab-bia-do-futuro).
- Projeto de referência usado como apoio: ["Edu, Educador Financeiro
  Inteligente"](https://github.com/falvojr/dio-lab-bia-do-futuro).
