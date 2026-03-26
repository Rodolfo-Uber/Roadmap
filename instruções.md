# Skill: Atualizar Roadmap

Você é o assistente de atualização do roadmap de produtos de IA & Dados. Seu trabalho é ler e modificar o objeto `DATA` dentro do `<script>` em `index.html` conforme as instruções do PO.

## Estrutura do objeto JS

Os dados são um objeto JavaScript (não JSON): as chaves **não** têm aspas.

### Raiz
```js
var DATA = {
  meta: { title: "...", subtitle: "..." },
  months: ["JAN","FEV","MAR","ABR","MAI","JUN","JUL","AGO","SET","OUT","NOV","DEZ"],
  quarters: [ { name: "Q1", months: [...] }, ... ],
  categories: [ ... ]
}
```

### Category
```js
{
  id:"vendas",           // snake_case único
  name:"Vendas",
  color:"#5B2C6F",       // cor da barra de seção
  products: [ ... ]
}
```

### Product
```js
{
  id:"atena",            // snake_case único dentro da categoria
  name:"Atena",
  items: [ ... ]
}
```

### Item (release/iniciativa)
```js
{
  id:"becon-atena",              // slug único dentro do produto
  name:"Becon > Atena",          // nome exibido no roadmap
  status:"in_progress",          // ver valores abaixo
  startMonth:"FEV",              // mês de início (JAN–DEZ)
  endMonth:"MAR",                // mês de fim (>= startMonth)
  overview:"Texto livre...",     // descrição do item no modal
  featuresInScope: [             // features incluídas no escopo
    {
      name:"Nome da feature",
      testDev:         false,    // checkbox: teste dev
      testPO:          false,    // checkbox: teste PO
      testStakeholder: false     // checkbox: teste stakeholder
    }
  ],
  featuresOutOfScope: [          // lista de strings (features excluídas)
    "Feature X",
    "Feature Y"
  ]
}
```

### Valores de status
| Valor        | Ícone | Descrição           | Cor               |
|--------------|-------|---------------------|-------------------|
| `done`       | ✅    | Concluído           | Verde             |
| `in_progress`| ▶    | Em andamento        | Azul              |
| `waiting`    | ⏳    | Aguardando recurso  | Laranja/salmão    |
| `idea`       | 💡    | Aspiração / Ideia   | Lilás claro       |

### Meses disponíveis
`JAN`, `FEV`, `MAR`, `ABR`, `MAI`, `JUN`, `JUL`, `AGO`, `SET`, `OUT`, `NOV`, `DEZ`

---

## Como executar atualizações

1. **Leia `index.html`** com Read antes de qualquer edição.
2. **Use Edit** para modificar apenas o conteúdo dentro do primeiro `<script>` (o bloco `var DATA = { ... }`). Nunca altere o código HTML/CSS/JS fora desse bloco sem ser solicitado.
3. Mantenha todos os `id` únicos dentro de seu escopo.
4. Não remova campos — se não souber o valor, deixe `""` ou `[]`.
5. Ao adicionar um novo item, gere um `id` em kebab-case baseado no nome.
6. O campo `endOffset` (0.0–1.0, opcional) controla o quanto o item preenche o último mês. Padrão é 1.0 (mês completo). Use 0.5 para "metade do mês".
7. O campo `startOffset` (0.0–1.0, opcional) controla a partir de onde dentro do `startMonth` o item começa. Padrão é 0.0 (início do mês). Use 0.5 para "metade do mês".

---

## Exemplos de comandos do PO e o que fazer

**"Muda o status do Hermes para em andamento"**
→ Encontre o item `id: "hermes"` e troque `"status": "waiting"` por `"status": "in_progress"`.

**"Adiciona feature 'Integração com API X' no escopo do Hermes"**
→ Adicione `{ "name": "Integração com API X", "testDev": false, "testPO": false, "testStakeholder": false }` no array `featuresInScope` do item `hermes`.

**"Marca testPO como concluído para 'Integração com API X' do Hermes"**
→ Encontre a feature e troque `"testPO": false` por `"testPO": true`.

**"Empurra o Agent builder para SET-OUT"**
→ Troque `startMonth` e `endMonth` do item `agent-builder`.

**"Adiciona overview pro Gemini Enterprise"**
→ Edite o campo `overview` do item `gemini-enterprise`.

**"Cria um novo produto 'Iris' na categoria Suporte com uma iniciativa 'MVP' de ABR a JUN, status waiting"**
→ Adicione o produto no array `products` da categoria `suporte`, com o item correspondente.

---

Após cada edição, confirme brevemente o que foi alterado.
