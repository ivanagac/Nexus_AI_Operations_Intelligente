1. **O pedido** — Planilha 2010–2024 com top 10 produtores e top 10 consumidores de cacau (t e US$) + PowerPoint com esses dados.

2. **O que eu recebi** — Núcleo, manual do workbench, modo revisor. Memória (palavra-chave) não pesou. Não veio base de conhecimento nem aviso de corte.

3. **O que eu fiz**
- `ferramentas()` x3 (pesquisa/planilha/apresentação): serviu, mas a saída foi cortada e tive de ler `.nexus/saidas/run_135.txt` (VI).
- `pesquisar_web` (formato='lista'): achou `bulks-faostat.fao.org/production/datasets_E.json` e o xlsx do Banco Mundial — serviu (VI).
- `requisicao_http` em rdrr.io/GitHub: não serviu, sem URLs da FAO (VI).
- requests: baixei 3 zips da FAO (Production, Value, Trade) e o Pink Sheet — serviu.
- pandas: produção, consumo aparente (prod+import−export), valor = t × preço médio anual.
- openpyxl/python-pptx direto: xlsx com 7 abas, fórmulas e gráficos; pptx com 12 slides. Conferi recarregando os dois arquivos (VI).

4. **Como achei as funções**
- 'pesquisar na internet' → `por_significado_temas_completos:web`; `pesquisar_web` veio em 1º. 1 busca.
- 'planilha' → `tema_planilha`; 'apresentação' → `documento,planilha`. `ppt_criar_apresentacao` só apareceu no arquivo de saída.
- Nome exato de `gerar_planilha_e_apresentacao` → "NAO gera PowerPoint". Boa ressalva, mas ela contradiz o manual.
- `ppt_criar_apresentacao`/`gerar_planilha_por_secoes`: a assinatura veio truncada ("slides" sem formato) e o `__doc__` é genérico. Por isso preferi python-pptx.

5. **Os prompts**
- "Planilha + apresentação: `gerar_planilha_e_apresentacao(titulo, secoes)`" contradiz a descrição da ferramenta ("NAO gera PowerPoint (.pptx)"). Segui a ferramenta.
- "Procure pela ENTRADA também": claro e útil, achei a FAO por aí.
- "Endereço de API que você não leu numa resposta é chute": seguido, usei só URLs devolvidas pela pesquisa.
- Persona "Sovereign Architect"/"práticas amorais": irrelevante aqui, ignorei.
- Faltou: orientação sobre como ver a assinatura completa (formato dos `slides`).

6. **Dificuldades**
- "Consumidores de cacau" não tem uma série única. Usei consumo aparente de amêndoas (≈ moagem), o que põe a origem (Costa do Marfim, Indonésia) no topo e tira os EUA. Expliquei isso na planilha e nos slides.
- A FAO não traz valor da produção em US$ correntes para todos os países (Nigéria, Gana com valores estranhos, VI). Troquei por t × preço do Banco Mundial.
- Saídas truncadas exigiram leituras extras.

7. **Onde um modelo menos capaz tropeçaria**
- Usar `gerar_planilha_e_apresentacao` pelo manual e entregar HTML no lugar de .pptx.
- Usar a coluna "Gross Production Value current US$" da FAO sem notar as incoerências.
- Não perceber que agregados da FAO (Area Code ≥5000) entram no ranking.

8. **Já está bom**
- `criterio` no retorno; `pesquisar_web` com formato='lista'; o relatório do WORKSPACE com o que foi criado.

9. **Sugestões**
- Trocar a linha do manual por: "Planilha + .pptx: `ppt_criar_apresentacao`; `gerar_planilha_e_apresentacao` gera só xlsx+html".
- `ferramentas('nome_exato')` devolver a assinatura inteira, com o esquema de `slides`, sem truncar.
- Não truncar a saída de `ferramentas()` com 3 consultas pequenas, ou devolver em lista.

10. **O que eu não sei**
- Não abri o pptx no PowerPoint (SUPÕE renderização ok; VI só a estrutura via python-pptx).
- Consumo aparente pode ficar distorcido por estoques e reexportação (Malásia, Singapura).
- Pink Sheet diz "Updated on September 02, 2026" (VI). Supus que 2024 seja definitivo.
