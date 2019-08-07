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

  return <button type="button" onClick={handleAdd}>Adicionar</button>
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

### useMemo
---
Exemplo de introdução:
```javascript
  return <strong>Você tem {tech.length} tecnologias</strong>
```
No exemplo acima, acessamos o tamanho do array com a função **length**..

O problema deste código é que ele renderiza toda vez que o **return** é chamado, ele é chamado sempre que qualquer tipo de **variável** que está sendo utlizada no componente é alterada, toda vez que inserirmos um valor dentro de um input controlado e etc... Por mais que um **.length** seja simples o **useMemo** é indicado para este tipo de ocasiões, no caso do nosso exemplo é muito simples mas varia de caso a caso, pode acontecer de ter um calculo muito mais complexo que chama outras funções e que podera afetar a performance caso seja muito complexo.

Exemplo 2:
```javascript
  const techSize = useMemo(() => tech.length, [tech]);

  return <strong>Você tem {techSize} tecnologias</strong>
```

No exemplo acima criamos uma variável para receber nossa função, no primeiro parâmetro passamos uma função e dentro desta função inserimos nosso bloco de código, e como de costume o segundo parâmetro passamos uma variável para ele ficar monitorando assim toda vez que houver alguma mudança nesta variável a função será executada e exibirá na tela o retorno da função

### useCallback
---
Na explição do hook **useState** no **Exemplo 2** criamos uma função chamada **handleAdd** ela é uma **function** que está sendo definida dentro de outra **function**, como ele esta declarada junto com os hooks ela sempre será montada toda vez que as variáveis do componente é alterada.
Exemplo: se eu adicionar alguma informação em algum array, digitar em um input controlado entre outros... ela sempre será criada novamente do zero, então isso acaba gastando **processamento do javascript** pois o javascript terá que apagar da memória e criar uma nova locação para criar ela novamente, no caso do nosso exemplo é uma função muito simples mas muitos casos pode acontecer de ser códigos mais complexos.

Exemplo 1:
```javascript
  const handleAdd = useCallback(() => {
    setTech([...tech, newTech]);
    setNewTech('');
  }, [newTech, tech]);
```

No exemplo acima, passamos de primeiro parâmetro uma função e dentro desta função inserimos o nosso bloco de código que será executado, no segundo parâmetro passamos as variáveis que o nosso bloco de código deverá ficar monitorando, ou seja, toda vez que tiver alguma alteração nas variáveis **newTech** e **tech** será executado o nosso trecho de código.
