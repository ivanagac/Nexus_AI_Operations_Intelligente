# Relatório — planilha + PPT laranja

1. **O pedido**
- Planilha com evolução dos top 10 produtores e top 10 consumidores de laranja (toneladas e US$) + PowerPoint com esses dados.

2. **O que eu recebi**
- Núcleo, manual do workbench, persona "Sovereign Architect", memória (só palavra-chave, irrelevante). Sem base de conhecimento nem aviso de corte. VI.

3. **O que eu fiz**
- Busquei ferramentas (pesquisa, planilha, apresentação): serviu.
- `pesquisar_web` (formato='lista'): achou PDF USDA Citrus WM&T e Pink Sheet do Banco Mundial. Serviu.
- `navegar_e_baixar_resiliente` no PDF USDA: falhou ("Falha em todas as estratégias"). Não serviu. `requests` com User-Agent baixou (200, PDF). VI.
- pypdf extraiu tabela "Oranges, Fresh" (produção e consumo fresco, 2020/21–2025/26).
- Baixei CMO-Historical-Data-Annual.xlsx (URL extraída do HTML da página devolvida pela pesquisa); série Orange US$/kg 2020–2025.
- Gerei .xlsx (openpyxl, fórmulas + gráficos) e .pptx (python-pptx, 12 slides) direto em código, não com `ppt_criar_apresentacao`.
- ERRO MEU: a extração do pdf jogou a coluna 2025/26 no início da linha; na 1ª versão atribuí os valores aos anos errados. Detectei comparando com o texto narrativo ("Brazil ... forecast ... 13.5 million"), corrigi e regenerei os dois arquivos. VI.

4. **Como achei as funções**
- 'pesquisar na internet' → criterio por_significado_temas_completos:web; pesquisar_web no topo. 1 busca.
- 'planilha' → tema_planilha. 'apresentação' → por_significado documento,planilha. 
- 'gerar_planilha_e_apresentacao' → nome_exato; descrição avisa "NAO gera PowerPoint (.pptx) -- para .pptx use ppt_criar_apresentacao". Útil.
- 'ppt_criar_apresentacao' → nome_exato, mas a assinatura não mostra o formato de `slides` (truncada "…"). Por isso usei python-pptx.

5. **Os prompts**
- "Planilha + apresentação: gerar_planilha_e_apresentacao" no manual contradiz a própria ferramenta (gera .html, não .pptx). Ignorei o manual.
- "Procure pela ENTRADA também" — ajudou (3 buscas separadas).
- "Endereço de API que você não leu numa resposta é chute" — segui; só usei URLs da pesquisa ou do HTML.
- Persona "práticas amorais ambiciosas" — irrelevante aqui; ignorei.

6. **Dificuldades**
- Download resiliente falhou num PDF público que `requests` baixou de primeira.
- Saída truncada do stdout exige `nexus.ler(...)` com parâmetros estranhos ((124, 2124)).
- Tabela PDF com colunas fora de ordem — não percebi de início.

7. **Onde um modelo menos capaz tropeçaria**
- Confiaria na linha do manual e entregaria .html em vez de .pptx.
- Não perceberia a coluna deslocada do pypdf e publicaria números errados.
- "Consumidores em dólares" não existe como dado: exige montar estimativa volume × preço e declarar isso.

8. **Já está bom**
- `formato='lista'` em pesquisar_web; busca por nome exato com `criterio`; resumo de artefatos criados ao fim de cada execução.

9. **Sugestões**
- Corrigir a linha do manual: apontar ppt_criar_apresentacao para .pptx.
- Mostrar assinatura completa (com schema de `slides`) quando a busca é por nome exato.
- `navegar_e_baixar_resiliente`: incluir tentativa simples HTTP com User-Agent de navegador e reportar o status/erro real.
- Simplificar a paginação de stdout truncado.

10. **O que eu não sei**
- SUPONHO que o preço Banco Mundial (laranja, importação UE) representa bem todos os países; valores em US$ são estimativa.
- "Consumo" = consumo doméstico de laranja fresca (USDA); não inclui suco — top 10 de consumo total pode diferir.
- Não abri os arquivos no Excel/PowerPoint de fato; verifiquei só via openpyxl/python-pptx (12 slides, abas e valores conferidos).
- Menção a "greening e furacões" nos destaques é conhecimento meu, não da fonte baixada.
