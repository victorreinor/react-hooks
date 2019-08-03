# React-hooks
A partir da versão 16.8 foi adicionado a API de hooks, esses hooks estão sendo muitos utilizados no react pois reduzem muito a verbosidade de muitas formas que a gente tinha antes no react para compartilhamento de informações entre componentes e também reduzem a verbosidade em bibiliotecas ex: Redux

### useState
---
É o hook que vai pertencer a uma função para gente criar estados na função sem escrever ela no formato de classe

Exemplo 1:
```javascript
  const [tech, setTech] = useState(['ReactJS', 'React Native']);
```

Definimos uma constante fazendo **destructuring** e como argumento para o **useState** passamos o valor inicial do estado.

O useState retorna um array por isso fazemos destructuring, na primeira posição retorna o estado e na segunda uma função que servirá para atualizar as informações do estado.

Então toda vez que quiser evoluir o estado será utilizado o segundo parametro como no exemplo a seguir.

Exemplo 2:
```javascript
  const [tech, setTech] = useState(['ReactJS', 'React Native']);

  function handleAdd() {
    setTech([...tech, 'NodeJS']);
  }

  return (
    <button type="button" onClick={handleAdd}>Adicionar</button>
  );
```
