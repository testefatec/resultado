# Guia de Contribuição - FATEC

## Para Alunos

Este guia explica como enviar seus resultados de atividades para este repositório.

## Métodos de Submissão

### Método 1: Interface Web do GitHub (Mais Fácil)

Este é o método recomendado para a maioria dos alunos.

1. **Acesse o repositório**: [https://github.com/testefatec/resultado](https://github.com/testefatec/resultado)

2. **Vá para a aba Actions**
   - Clique na aba "Actions" no topo da página

3. **Selecione o workflow correto**
   - Na lista à esquerda, clique em "Receber Resultados de Alunos"

4. **Execute o workflow**
   - Clique no botão "Run workflow" (no lado direito, em verde)
   
5. **Preencha o formulário**:
   - **Nome do Aluno**: Seu nome completo (ex: "Maria da Silva")
   - **RA do Aluno**: Seu número de RA (ex: "12345678")
   - **Nome da Atividade**: Código ou nome da atividade (ex: "Lab01", "Trabalho_Final")
   - **Resultado da Atividade**: 
     - Pode ser texto simples
     - Pode ser JSON: `{"nota": 10, "comentario": "Excelente trabalho"}`
     - Pode ser uma URL do seu repositório
     - Pode ser um resumo do que foi feito

6. **Confirme a submissão**
   - Clique em "Run workflow" (botão verde)
   - Aguarde alguns segundos
   - Seu resultado será salvo automaticamente no repositório

### Método 2: Usando a API do GitHub

Para alunos mais avançados que querem automatizar o envio:

```bash
#!/bin/bash

# Configuração
GITHUB_TOKEN="seu_token_aqui"
STUDENT_NAME="Seu Nome"
STUDENT_ID="12345678"
ASSIGNMENT="Lab01"
RESULT="Seu resultado aqui"

# Enviar resultado
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token $GITHUB_TOKEN" \
  https://api.github.com/repos/testefatec/resultado/actions/workflows/receive-results.yml/dispatches \
  -d "{
    \"ref\": \"main\",
    \"inputs\": {
      \"student_name\": \"$STUDENT_NAME\",
      \"student_id\": \"$STUDENT_ID\",
      \"assignment\": \"$ASSIGNMENT\",
      \"result\": \"$RESULT\"
    }
  }"
```

**Nota**: Para usar este método, você precisará criar um Personal Access Token no GitHub com permissões de `workflow`.

### Método 3: Integração com seu Workflow

Se você tem seu próprio workflow no GitHub Actions, pode integrar o envio de resultados:

```yaml
name: Meu Workflow com Envio de Resultados

on: [push]

jobs:
  meu-teste:
    runs-on: ubuntu-latest
    steps:
      - name: Executar meus testes
        id: test
        run: |
          # Seus testes aqui
          echo "result=Teste passou com sucesso" >> $GITHUB_OUTPUT
      
      - name: Enviar resultado (manual)
        run: |
          echo "Resultado: ${{ steps.test.outputs.result }}"
          echo "Copie este resultado e envie para o repositório de resultados"
```

## Formato Recomendado para Resultados

### Resultado Simples (Texto)
```
Atividade concluída com sucesso.
Todos os testes passaram.
```

### Resultado Estruturado (JSON)
```json
{
  "status": "sucesso",
  "testes_executados": 10,
  "testes_passaram": 10,
  "testes_falharam": 0,
  "tempo_execucao": "2.5s",
  "observacoes": "Todos os requisitos foram atendidos"
}
```

### Resultado com Link
```
Repositório: https://github.com/seu-usuario/seu-projeto
Status: Completo
Commit: abc123def456
```

## Verificando seu Resultado

Após enviar seu resultado:

1. Aguarde alguns segundos para o workflow processar
2. Vá para a aba "Actions" e verifique se o workflow "Receber Resultados de Alunos" executou com sucesso
3. Seu resultado estará salvo no diretório `results/` do repositório
4. O nome do arquivo seguirá o padrão: `RA_Atividade_DataHora.txt`

## Problemas Comuns

### "Workflow não aparece na lista"
- Certifique-se de estar no repositório correto: `testefatec/resultado`
- Verifique se você tem acesso ao repositório

### "Erro ao executar workflow"
- Verifique se preencheu todos os campos obrigatórios
- Certifique-se de que seu RA contém apenas números
- Se o problema persistir, contate o professor

### "Não encontro meu resultado"
- Aguarde alguns minutos após a submissão
- Verifique o diretório `results/` no repositório
- Procure por um arquivo com seu RA no nome

## Suporte

- Para dúvidas sobre o uso: Consulte este guia ou o README.md
- Para problemas técnicos: Abra uma issue ou contate o professor
- Para dúvidas sobre a atividade: Contate seu professor

## Boas Práticas

1. **Teste antes de enviar**: Certifique-se de que seu resultado está correto
2. **Seja claro**: Use descrições objetivas no campo "Resultado"
3. **Mantenha organizado**: Use nomes consistentes para suas atividades
4. **Envie apenas uma vez**: Evite submissões duplicadas
5. **Inclua informações relevantes**: Data, status, links importantes

## Exemplo Completo

```
Nome do Aluno: João da Silva
RA: 12345678
Atividade: Lab03_API_REST
Resultado:
{
  "status": "completo",
  "repositorio": "https://github.com/joao/lab03-api",
  "endpoints_implementados": 5,
  "testes_unitarios": "100% de cobertura",
  "observacoes": "API REST implementada conforme especificação"
}
```
