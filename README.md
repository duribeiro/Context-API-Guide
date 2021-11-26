# Context-Api-guide
Guia prático de como configurar e usar o Context API do React para iniciantes.

Consulte a [documentação do Context Api](https://pt-br.reactjs.org/docs/context.html) pra explicações mais detalhadas.

O Contexto (context) fornece uma forma de compartilhar dados, entre todos componentes da mesma árvore de componentes, sem precisar passar via props de pai pra filho, neto, irmão, etc.. entre os vários níveis da árvore de componentes.

Contexto (context) é usado principalmente quando algum dado precisa ser acessado por muitos componentes em diferentes níveis.

# Criando um contexto

```js
// src/context/MyContext.js

import React, { createContext } from 'react';

const MyContext = createContext(defaultValue);

export default MyContext;
```
O `defaultValue` é meio que um valor padrão de backup, pois o compontente que vai utilizar o `MyContext` só vai conseguir ler esse "valor padrão" quando não encontrar um `provider` na sua arvore de componentes.
