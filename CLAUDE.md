# Gradua: instruções para o Claude

App de estudos de graduação. Arquivo único `index.html`, sem build, sem backend e sem dependências além da fonte do Google Fonts.

## Regras do projeto (obrigatórias)
- O app **não usa IA em tempo de execução**. Todo conteúdo é texto fixo no código. Não adicione chamadas de rede para gerar ou buscar conteúdo.
- Escreva em português do Brasil. Textos **originais**: nunca copie trechos de livros, artigos ou sites.
- Referências: somente obras reais e conhecidas. **Nunca invente** autor, título, edição, ano ou página. Se não tiver certeza de um dado, omita-o (ex.: cite só autor, título e editora).
- Conteúdo de saúde e de direito deve ser revisado por um profissional antes de ser divulgado.
- Não existe "Em produção" em disciplina que já tenha conteúdo. Disciplina sem conteúdo em `D` aparece como "Em produção"; isso é proposital.

## Onde fica cada coisa em `index.html`
- `COURSES`: cursos (`id`, `n` nome, `i` emoji, `c` cor, `s` lista de `"Disciplina|semestre"`). As grades são ajustadas pelos blocos `L` e `L2` e pela lista de cursos novos, mais abaixo no script. Ciência da Computação, Odontologia e Arquitetura vêm do currículo oficial da UFSC (marcados em `VER`).
- `G` e `SRC` (logo antes de `D["Cálculo 1"]=...`): grade final de cada curso e universidades usadas. Ela substitui `L`/`L2` e é a união das disciplinas obrigatórias das matrizes oficiais de UFSC, UDESC, UFFS, Unochapecó, FURB, Univali e Unisul. Os dados brutos, com links das fontes, ficam em `dados/grades/<id>.json`. Unochapecó e Univali bloquearam a leitura automática e ainda faltam.
- `D`: conteúdo de cada disciplina. A **chave deve ser idêntica ao nome da disciplina** na grade (ex.: `"Cálculo 1"`).
- `X`: mapas mentais extras por disciplina (opcional).
- `LB`: biblioteca por disciplina (vídeos por assunto, livros, artigos).
- Funções principais: `render`, `home`, `course`, `list`, `learn`, `practice`, `lib2`.

## Formato de uma disciplina em `D`
```js
"Nome da disciplina": {
  rp: ["parágrafo 1", "..."],            // resumo: 5 parágrafos ou mais
  res: ["ponto-chave", "..."],           // lista de pontos-chave do resumo
  exp: ["parágrafo 1", "..."],           // explicação: 5 parágrafos ou mais
  ref: ["SOBRENOME, N. <em>Título</em>. Cidade: Editora.", "..."],
  map: ["Assunto central", [["Ramo", ["folha", "folha"]], ["Ramo", ["folha"]]]],
  caso: ["contexto do caso", "pergunta", "resposta comentada"],
  q: { f: [["enunciado", ["a","b","c"], indiceDaCorreta]], m: [], d: [] } // fácil, médio, difícil
}
```
Para mais mapas, adicione em `X["Nome da disciplina"] = [ [raiz, [[ramo, [folhas]]]], ... ]`.
Para a biblioteca: `LB["Nome"] = { v: [[tópico, descrição]], b: [[título, autor, descrição]], a: [[tópico, descrição]] }`.
Adicione novas entradas de `D` dentro do objeto `const D={...}`.

## Metas de conteúdo por disciplina
Resumo e explicação com 5+ parágrafos e referências; 4+ mapas mentais; 20 casos; provas nos 3 níveis. Hoje só 3 disciplinas têm texto completo e as metas de casos e questões ainda não foram atingidas. Priorize qualidade e fidelidade às referências, não volume.

## Como testar
Abra `index.html` no navegador. Confira: tela inicial, lista do curso, as 4 abas da disciplina (Aprender com resumo, mapa, explicação e caso; Praticar; Biblioteca; Progresso) e o modo escuro.
