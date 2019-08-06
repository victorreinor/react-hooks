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

### useEffect
---
Ele sobrepõe os métodos do ciclo de vida dos componentes **componentDidMount, componentDidUpdate, componentWillUnmount**

Exemplo 1: componentDidUpdate
```javascript
  useEffect(() => {
    localStorage.setItem('tech', JSON.stringify(tech));
  }, [tech]);
```

Primeiro parâmetro que o **useEffect** recebe é uma função que será executada e o segundo e quando ela vai ser executado, ou seja, o segundo parâmetro é um array de dependencias, ele fica monitorando alterações em certas variáveis, nesse caso do exemplo a cima deixamos ele monitorando a variavel **tech** e caso aja alguma alteração ele inclui no localStorage do browser

Exemplo 2: componentDidUpdate
```javascript
  useEffect(() => {
    const storageTech = localStorage.getItem('tech');

    if (storageTech) setTech(JSON.parse(storageTech));
  }, []);
```

No exemplo acima deixamos o segundo parâmetro vazio pois queremos que ele só executa quando o componente montar e recuperamos todas as informações já salvas no localStorage, fazendo assim o papel do **componentDidMount**

Exemplo 3: componentWillUnmount
```javascript
  useEffect(() => {
    return () => {
      /*
        bloco de código
      */
    };
  }, []);
```

Para fazer o papel do **componentWillUnmount** precisamos só de colocar um return com uma função como monstra o exemplo a cima.
