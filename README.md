# Hidratação de manutenção (Holliday-Segar)

Identificador: `holliday-segar`. Pacote independente da interface ELUCENIA, para navegador e Node.js.

## Situação

- Revisão: **restricted**. A entrada só solicita peso e não verifica idade nem exclusões. A diretriz AAP citada abrange 28 dias–18 anos e exclui, entre outros, câncer, disfunção renal e cardiopatia. Há recomendação de restrição de volume sem avaliação clínica; suspender aplicação assistencial e manter documentação.
- Execução: **desativada; o adaptador retorna REVIEW_REQUIRED**.
- Validação clínica independente: **não realizada**. Os testes abaixo verificam aritmética e transporte dos campos.
- Fonte importada: Panorama Médico; arquivo `app/content/ferramentas/mulher-crianca.php`.
- 4/4 casos de referência conferidos na importação. 0 casos independentes desta ferramenta.
- Dados: o exemplo funciona localmente, sem rede, armazenamento ou identificação de pacientes.

## Uso no Node.js

```js
const { calculate } = require('./calculator.js');
const example = require('./examples.json')[0];
console.log(calculate(example.input));
```

Execute `node test.cjs` (ou `npm test`) para conferir os exemplos. Abra `index.html` para usar a versão local do navegador. Não há dependências npm.

## Contrato

`calculate(input)` recebe um objeto, devolve `{id, main, label, raw, clinicalValidation}` ou `{error, code, field?}`. Consulte `tool.json` e `metadata.fields` para nomes, unidades, opções e intervalos. Números aceitam valores finitos ou strings numéricas; opções precisam corresponder às chaves documentadas. Campos obrigatórios vazios, booleanos inválidos, valores fora de intervalo e resultados não finitos são rejeitados. Somente checkbox omitido representa falso; um campo numérico ou uma opção obrigatória nunca é preenchido automaticamente.

Interpretações, ordens terapêuticas e tabelas herdadas não são retornadas pelo adaptador. Classificações e valores ainda dependem da população e das limitações da fonte.

## Fórmula / versão

Estimativa histórica de manutenção: 100 mL/kg/dia nos primeiros 10 kg; 50 nos próximos 10; 20 por kg adicional. A regra horária 4–2–1 é uma aproximação distinta. Não determina reposição, composição ou prescrição.

A transcrição acima documenta o acervo de origem e pode requerer atualização. Revisão documental: https://publications.aap.org/pediatrics/article/142/6/e20183083/37529/Clinical-Practice-Guideline-Maintenance

## Condições e limites

Estima o volume de manutenção de líquidos por dia e por hora pelo peso, base para prescrever hidratação venosa em crianças.

Confirme população, exclusões, unidades, versão e diretriz aplicável ao país e serviço. O resultado não deve ser utilizado isoladamente para diagnóstico, alta ou prescrição. O pacote não representa certificação clínica, aprovação regulatória ou indicação para toda população. Veja a revisão completa em `tool.json`.

## Fontes originais

- [Holliday MA, Segar WE. The maintenance need for water in parenteral fluid therapy. Pediatrics, 1957.](https://doi.org/10.1542/peds.19.5.823)
- [Feld LG et al. Clinical Practice Guideline: Maintenance Intravenous Fluids in Children. Pediatrics, 2018.](https://doi.org/10.1542/peds.2018-3083)

## Exemplos e rastreabilidade

`examples.json` preserva `originalInput`, expectativa e entrada explícita do exemplo. Não foi necessário expandir opções zero nos exemplos.

## Direitos e repositório

Este pacote integra o acervo privado de desenvolvimento da ELUCENIA. A publicação externa depende de liberação expressa. A licença MIT (arquivo LICENSE) cobre o código de integração, preservando o aviso de autoria e a licença; não transfere direitos sobre instrumentos, traduções, questionários, artigos, marcas ou outros materiais de terceiros. Consulte NOTICE.md e as condições de cada titular. O acesso a este adaptador não publica nem licencia automaticamente o restante da plataforma ELUCENIA.

## Acesso ao repositório

Repositório privado da organização ELUCENIA. A abertura pública depende de liberação expressa.
