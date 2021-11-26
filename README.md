# Context-API-guide
Guia prático de como configurar e usar o Context API do React para iniciantes.

Consulte a [documentação do Context Api](https://pt-br.reactjs.org/docs/context.html) pra explicações mais detalhadas.

O Contexto (context) fornece uma forma de compartilhar dados, entre todos componentes da mesma árvore de componentes, sem precisar passar via props de pai pra filho, neto, irmão, etc.. entre os vários níveis da árvore de componentes.

Contexto (context) é usado principalmente quando algum dado precisa ser acessado por muitos componentes em diferentes níveis.

# Criando um contexto

```js
// src/context/MyContext.js

import { createContext } from 'react';

const MyContext = createContext(defaultValue);

export default MyContext;
```
A função `creatContext()` retorna um objeto com das chaves um `Provider`e um `Consumer`, no código acima esse objeto está armazenado na const `MyContex`.

O `defaultValue` é meio que um valor padrão de backup, pois o compontente que vai utilizar o `MyContext` só vai conseguir ler esse "valor padrão" quando não encontrar um `Provider` acima dele arvore de componentes.

O `Provider` é o provedor dos dados ele dá acesso aos componentes que estão abaixo dele na arvore de componentes, geralmente ele envolve o componente pai de todos, ex: `index.js` ou o `App.js`
Já o `Consumer` é utilizado sempre que um componente precisa "consumir" o valor do contexto.

# Criando um provider simples

Importamos o `Provider` diretamente dentro do componente pai (pode ser o `index.js`, `App.js` ou outro componente).

```js
// src/components/MyComponent.js

import React from 'react';
import MyContext from '../context/MyContext';

function MyComponent() {
  return (
    <MyContext.Provider value={123}>
      <MyOtherComponent />
    </MyContext.Provider>
  )
}

export default MyComponent;
```

# Criando um provider reutilizável

Para essa forma mais avançada usamos a [composição de componente](https://pt-br.reactjs.org/docs/composition-vs-inheritance.html) no `provider` e o exportamos ao final. Dessa maneira ele se torna um componente genérico que pode ser importado em qualquer lugar e receber como filho especificamente o componente que vai ultizar os dados do contexto, independente da hierarquia na arvore de componente.\
A vantagem é evitar a re-renderização de todos os componentes filhos cada vez que a uma informação for atualizada no contexto. [Exemplos de uso](#exemplos-de-uso)

```js
// src/context/MyProvider.js

import React from 'react';
import PropTypes from 'prop-types';
import MyContext from './MyContext';

function MyProvider({ children }) {
  const contextValue = {
    number: 1,
    string: 'Hello world!',
    object: {},
    array: [],
    function: myFunction(),
  };

  return (
    <MyContext.Provider value={ contextValue }>
      {children}
    </MyContext.Provider>
  );
}

MyProvider.propTypes = {
  children: PropTypes.element.isRequired,
};

export default MyProvider;
```
# Exemplos de uso
