# Histórico de Bugs — wemove-landing

Registro de bugs identificados em produção ou testes, com análise e correção aplicada.
Formato: severidade (🔴 crítico · 🟠 alto · 🟡 médio · 🟢 baixo)

---

## BUG-LAND-001 🔴 ERR_TOO_MANY_REDIRECTS ao acessar wemoveapp.co
**Data:** 2026-04-25  
**Commit de correção:** (vercel.json simplificado para `{}`)

### Ocorrência
Após apontar o domínio `wemoveapp.co` para o projeto no Vercel, o acesso pelo domínio resultava em `ERR_TOO_MANY_REDIRECTS`. O site carregava normalmente pelo subdomínio padrão da Vercel (`wemove-landing-delta.vercel.app`).

### Análise
O `vercel.json` configurava um redirect de `www.wemoveapp.co` → `wemoveapp.co` via regra de `redirects`. O Vercel já aplica esse mesmo redirect nativamente para domínios configurados no painel — a regra manual criava um loop:

```
wemoveapp.co → (Vercel nativo) → wemoveapp.co → (regra manual) → wemoveapp.co → ...
```

### Correção
`vercel.json` simplificado para `{}` (objeto vazio), deixando o Vercel gerenciar redirects www→apex nativamente sem conflito.
