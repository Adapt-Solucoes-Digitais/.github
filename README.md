# .github da Adapt

Este repositório é público de propósito: o GitHub só aplica os arquivos padrão de uma organização quando eles moram num `.github` público. Não tem segredo nenhum aqui.

| Pasta ou arquivo | Para que serve |
|---|---|
| `profile/` | O README que aparece na página da org. |
| `CONTRIBUTING.md` e `SECURITY.md` | Valem para todo repositório da org que não tiver os seus. |
| `.github/ISSUE_TEMPLATE/` e `.github/PULL_REQUEST_TEMPLATE.md` | Modelos de issue (ajuste, bug, pendência do cliente) e o checklist de PR. Também valem para a org inteira. |
| `.github/workflows/` | Workflows reutilizáveis: `qualidade.yml` (build, typecheck, testes e lint) e `publicar-cloudflare.yml` (deploy com Wrangler). |
| `workflow-templates/` | O modelo **Adapt · Site**, que aparece em *Actions → New workflow* em qualquer repositório da org. |

## Usando os workflows num projeto

```yaml
jobs:
  qualidade:
    uses: Adapt-Solucoes-Digitais/.github/.github/workflows/qualidade.yml@main

  publicar:
    needs: qualidade
    if: github.ref == 'refs/heads/main' && github.event_name == 'workflow_dispatch'
    uses: Adapt-Solucoes-Digitais/.github/.github/workflows/publicar-cloudflare.yml@main
    with:
      destino: workers
    secrets: inherit
```

As entradas de cada workflow estão documentadas no topo do próprio arquivo. Os segredos `CLOUDFLARE_API_TOKEN` e `CLOUDFLARE_ACCOUNT_ID` ficam em cada repositório, porque no plano gratuito segredo da org não chega em repositório privado.
