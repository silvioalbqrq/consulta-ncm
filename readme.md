# Consulta NCM × TIPI — Painel Contábil

Site estático e offline para consultar **NCM, EX, descrição e alíquota de IPI** conforme a TIPI 2022.

## Fonte

- Arquivo base: `1 TIPI 2022 - Atualizada ADE 001-2026.xlsx`
- TIPI 2022 (Decreto nº 11.158/2022), atualizada até **ADE RFB nº 1/2026**
- **Atualização 23/09/2026 — IT NF-e 2024.001 v2.40 / Res. Gecex nº 926 (vig. 01/10/2026):**
  - Inclusão: `8518.10.20 - Outros microfones, sem suporte` (desdobro de `8518.10.90`, TEC II 0%; IPI herdado de `8518.10.90` = 9,75% até ADE RFB de adequação da TIPI)
  - Descrição: `3913.90.50` passa de `Quitosan (Chitosan)...` para `Quitosana, seus sais ou seus derivados` (TEC 12,6% mantido)
  - Sem extinção/revogação de NCM nesta versão; reduções de TEC (8452.10.00, 9202.10.00, 9202.90.00, 9205.10.00, 9205.90.00) e exclusões do Anexo II da Res. Gecex 272 não alteram a validade dos NCM na NF-e
- Conversão direta do Excel, sem curadoria manual de texto

## Conteúdo da base

- **15.654 linhas**: 15.653 base + 1 inclusão (8518.10.20)
- **11.109** NCMs completas de 8 dígitos + **4.545** agrupamentos/títulos
- **15.064** códigos distintos (alguns NCMs repetem com EX diferente)
- **587** linhas com EX (inclui 5 desdobramentos `EX 01` cuja coluna NCM vinha em branco na planilha e herdaram o NCM anterior)
- `NT` = Não Tributado

## Arquivos

| Arquivo | O quê |
|---|---|
| `index.html` | Interface (painel contábil: KPIs + filtros + tabela densa + exportação) |
| `tipi-data.js` | Base (`const TIPI_DATA`) carregada via `<script>`, funciona em `file://` |
| `tipi-data.json` | Mesma base em JSON, para reuso |
| `readme.md` | Este arquivo |

## Como usar

1. Abra `index.html` em qualquer navegador (não precisa de servidor nem internet).
2. Busque por NCM com ou sem ponto (`8471`, `2208.30.10`) ou por descrição (`cerveja`, `queijo minas` — ignora acento/maiúscula).
3. Combine filtros: alíquota, EX, capítulo (2 primeiros dígitos) e tipo.
4. Clique no cabeçalho da tabela para ordenar; `/` foca a busca.
5. Clique no NCM para copiar; **Exportar CSV** baixa o filtro atual (`;`, UTF-8 com BOM).

## Manutenção / regeneração

A base foi gerada do Excel com herança de NCM para as 5 linhas `EX 01` sem NCM. Para regerar após nova TIPI, repetir a conversão e sobrescrever `tipi-data.js` / `tipi-data.json` mantendo o mesmo schema:

```json
[{ "ncm": "2208.30.10", "ex": "", "desc": "...", "aliq": "19.5", "digits": "22083010", "tipo": "item" }]
```
