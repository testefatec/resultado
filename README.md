# Resultado - Repositório de Resultados FATEC

## Sobre este Repositório

Este repositório foi criado para receber e armazenar resultados de workflows de alunos da FATEC.

## Como Funciona

Os alunos podem enviar seus resultados de atividades através do workflow automatizado disponível neste repositório.

## Estrutura

```
resultado/
├── .github/
│   └── workflows/
│       └── receive-results.yml   # Workflow para receber resultados
├── results/                       # Diretório onde os resultados são armazenados
└── README.md                      # Este arquivo
```

## Como Enviar Resultados

### Opção 1: Via Interface do GitHub (Recomendado)

1. Acesse a aba **Actions** neste repositório
2. Selecione o workflow **"Receber Resultados de Alunos"**
3. Clique em **"Run workflow"**
4. Preencha os campos:
   - **Nome do Aluno**: Seu nome completo
   - **RA do Aluno**: Seu número de RA
   - **Nome da Atividade**: Nome/código da atividade (ex: "Lab01", "Trabalho_Final")
   - **Resultado da Atividade**: Seu resultado (pode ser JSON, texto, URL, etc.)
5. Clique em **"Run workflow"** para enviar

### Opção 2: Via API do GitHub

Os alunos também podem enviar resultados programaticamente usando a API do GitHub:

```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token SEU_TOKEN" \
  https://api.github.com/repos/testefatec/resultado/actions/workflows/receive-results.yml/dispatches \
  -d '{
    "ref": "main",
    "inputs": {
      "student_name": "João Silva",
      "student_id": "12345678",
      "assignment": "Lab01",
      "result": "Teste executado com sucesso"
    }
  }'
```

## Formato dos Resultados

Os resultados são salvos no diretório `results/` com o seguinte formato de nome:

```
RA_NomeAtividade_DataHora.txt
```

Exemplo: `12345678_Lab01_20231119_143022.txt`

## Para Professores

Os resultados submetidos pelos alunos ficam armazenados no diretório `results/` e podem ser acessados através do repositório. Cada submissão inclui:

- Nome do aluno
- RA do aluno
- Nome da atividade
- Data e hora da submissão
- Resultado/conteúdo enviado pelo aluno

## Suporte

Em caso de dúvidas ou problemas, entre em contato com o professor responsável ou abra uma issue neste repositório.

## Licença

Este repositório é mantido pela FATEC para fins educacionais.