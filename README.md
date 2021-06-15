
# 💻 Sobre o desafio

Nesse desafio, você deverá criar uma aplicação para treinar o que aprendeu até agora no ReactJS

Essa será uma aplicação onde o seu principal objetivo é criar um hook de carrinho de compras. Você terá acesso a duas páginas, um componente e um hook para implementar as funcionalidades pedidas nesse desafio:

- Adicionar um novo produto ao carrinho;
- Remover um produto do carrinho;
- Alterar a quantidade de um produto no carrinho;
- Cálculo dos preços sub-total e total do carrinho;
- Validação de estoque;
- Exibição de mensagens de erro;
- Entre outros.


## 🚀 Começando

Essas instruções permitirão que você obtenha uma cópia do projeto em operação na sua máquina local para fins de desenvolvimento e teste.

Consulte **Implantação** para saber como implantar o projeto.

### 📋 Pré-requisitos

De que coisas você precisa para instalar o software e como instalá-lo?

```
Dar exemplos
```

### 🔧 Instalação

### Fake API com JSON Server

Assim como utilizamos o MirageJS no módulo 2 para simular uma API com os dados das transações da aplicação dt.money, vamos utilizar o JSON Server para simular uma API que possui as informações dos produtos e do estoque. 

Navegue até a pasta criada, abra no Visual Studio Code e execute os seguintes comandos no terminal:

```bash
yarn
yarn server
```

Em seguida, você vai ver a mensagem:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9111a286-7fbf-45de-8256-20a1790f3686/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9111a286-7fbf-45de-8256-20a1790f3686/Untitled.png)

Perceba que ele iniciou uma fake API com os recursos `/stock` e `/products` em `localhost` na porta `3333` a partir das informações do arquivo [server.json](https://github.com/rocketseat-education/ignite-template-reactjs-criando-um-hook-de-carrinho-de-compras/blob/master/server.json) localizado na raiz do seu projeto. Acessando essas rotas no seu navegador, você consegue ver o retorno das informações já em JSON:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0fe33995-e128-480c-aaf9-c8d77e0f5544/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0fe33995-e128-480c-aaf9-c8d77e0f5544/Untitled.png)

Para acessar a listagem de todos os produtos e estoque, basta realizar uma requisição GET nas rotas `/products` e `/stock` respectivamente. Para acessar os dados de um único item utilize os `route params`, exemplo: `/products/1` e `/stock/1` para acessar os dados do produto e estoque do produto de id 1, respectivamente.

## ⚙️ Executando os testes
>>yarn test
 Oque deve ser testado?

 - **should be able to render the amount of products added to cart**

Para que esse teste passe você deve renderizar o valor correto da quantidade de **tipos** de produtos 

```jsx
[
	{
	  amount: 2,
	  id: 1,
	  image:
	    'https://rocketseat-cdn.s3-sa-east-1.amazonaws.com/modulo-redux/tenis1.jpg',
	  price: 179.9,
	  title: 'Tênis de Caminhada Leve Confortável',
	},
	{
	  amount: 1,
	  id: 2,
	  image:
	    'https://rocketseat-cdn.s3-sa-east-1.amazonaws.com/modulo-redux/tenis2.jpg',
	  price: 139.9,
	  title: 'Tênis VR Caminhada Confortável Detalhes Couro Masculino',
	},
]
```

- **should be able to render each product quantity added to cart**

    Para que esse teste passe você deve renderizar corretamente a quantidade adicionada de cada produto adicionado ao carrinho dentro da tag `<div data-testid="cart-product-quantity">`. Sugerimos criar uma variável `cartItemsAmount` utilizando o método `reduce` para iterar sobre os produtos adicionados ao `cart` e gerar um array com o `

    Sugerimos criar uma variável `cartItemsAmount` utilizando o método `reduce` para iterar sobre os produtos adicionados ao `cart` e gerar um array com o `id` do produto e a quantidade adicionada ao carrinho. Exemplo:

    ```jsx
    [
    	0: 0,
    	1: 2,
    	2: 4
    ]
    ```

    Mostraria a quantidade 0 para o produto de `id` 1, 2 para o de `id e 4 para o último.

- **should be able to add a product to cart**

    Para que esse teste passe você deve clicar no botão `ADICIONAR AO CARRINHO` e o produto escolhido ser adicionado com sucesso ao carrinho. Além disso, a quantidade do produto no carrinho mostrada no botão deve representar o novo valor (incrementado de 1 unidade).

    - **should be able to increase/decrease a product amount**

    Para que esse teste passe você deve renderizar corretamente o valor da quantidade de cada produto adicionado ao carrinho e ser capaz de incrementar e decrementar os valores ao clicar

    no botões `<button *data-testid*="increment-product">` e `<button *data-testid*="decrement-product">` respect

- **should not be able to decrease a product amount when value is 1**

    Para que esse teste passe você deve desabilitar o botão `<button*data-testid*="decrement-product">` quando a quantidade do produto for igual a 1.

- **shoud be able to remove a product**

    Para que esse teste passe você deve ser capaz de remover o produto do carrinho ao clicar no botão `<button*data-testid*="remove-product">`

O valor correto a ser exibido é `2 itens`.



- **should be able to initialize cart with localStorage value**

    Para que esse teste passe você deve inicializar o estado `cart` com o valor da key `@RocketShoes:cart` do localStorage caso ele exista.

- **should be able to add a new product**

    Para que esse teste passe você deve utilizar a função `addProduct` para adicionar um novo produto ao carrinho e preservar o valor atualizado do carrinho no localStorage utilizando o `setItem`.

- **should not be able add a product that does not exist**

    Para que esse teste passe você deve utilizar a função `addProduct` para verificar que o produto não existe, mostrar um `toast.error` com a mensagem `Erro na adição do produto` e sair da função sem alterar o `cart` e o valor no localStorage.

- **should be able to increase a product amount when adding a product that already exists on cart**

    Para que esse teste passe você deve utilizar a função `addProduct` para incrementar em 1 unidade a quantidade de um produto no carrinho em vez de adicionar um novo produto. Deve também preservar o valor atualizado do carrinho no localStorage utilizando o `setItem`.

- **should not be able to increase a product amount when running out of stock**

    Para que esse teste passe você deve utilizar a função `addProduct` para verificar que a quantidade desejada do produto não possui em estoque (rota `stock/id` da Fake API). Deve também mostrar um `toast.error` com a mensagem `Quantidade solicitada fora de estoque` e sair da função sem alterar o `cart` e o valor no localStorage.

- **should be able to remove a product**

    Para que esse teste passe você deve utilizar a função `removeProduct` para remover um produto do carrinho. Deve também preservar o valor atualizado do carrinho no localStorage utilizando o `setItem`.

- **should not be able to remove a product that does not exist**

    Para que esse teste passe você deve utilizar a função `removeProduct` para verificar que o produto não existe no carrinho e mostrar um `toast.error` com a mensagem `Erro na remoção do produto`. Deve também sair da função sem alterar o `cart` e o valor no localStorage.

- **should be able to update a product amount**

    Para que esse teste passe você deve utilizar a função `updateProductAmount` para incrementar e decrementar o valor de um produto no carrinho. Deve também preservar o valor atualizado do carrinho no localStorage utilizando o `setItem`.

- **should not be able to update a product that does not exist**

    Para que esse teste passe você deve utilizar a função `updateProductAmount` para verificar que o produto não existe e mostrar um `toast.error` com a mensagem `Erro na alteração de quantidade do produto`. Deve também sair da função sem alterar o `cart` e o valor no localStorage.

- **should not be able to update a product amount when running out of stock**

    Para que esse teste passe você deve utilizar a função `updateProductAmount` para verificar que a quantidade desejada do produto não possui em estoque (rota `stock/id` da Fake API). Deve também mostrar um `toast.error` com a mensagem `Quantidade solicitada fora de estoque` e sair da função sem alterar o `cart` e o valor no localStorage.

- **should not be able to update a product amount to a value smaller than 1**

    Para que esse teste passe você deve utilizar a função `updateProductAmount` para verificar que a quantidade desejada do produto é menor que 1 e sair imediatamente da função sem alterar o `cart` e o valor no localStorage.





## 📦 Como deve ficar a aplicação

![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f166455c-a42f-4d25-8baa-a6686a3cb476/challenge.mp4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210615%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210615T104944Z&X-Amz-Expires=86400&X-Amz-Signature=fd0be7e7fcb6e3a7bbc2eb769f4707019be02c2b1c894a0a32e2eb9d401e31e2&X-Amz-SignedHeaders=host]

## 🛠️ Construído com

Mencione as ferramentas que você usou para criar seu projeto

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - O framework web usado
* [Maven](https://maven.apache.org/) - Gerente de Dependência
* [ROME](https://rometools.github.io/rome/) - Usada para gerar RSS

## 🖇️ Colaborando

Por favor, leia o [COLABORACAO.md](https://gist.github.com/usuario/linkParaInfoSobreContribuicoes) para obter detalhes sobre o nosso código de conduta e o processo para nos enviar pedidos de solicitação.

## 📌 Versão

Nós usamos [SemVer](http://semver.org/) para controle de versão. Para as versões disponíveis, observe as [tags neste repositório](https://github.com/suas/tags/do/projeto). 

## ✒️ Autores

Mencione todos aqueles que ajudaram a levantar o projeto desde o seu início

* **Um desenvolvedor** - *Trabalho Inicial* - [umdesenvolvedor](https://github.com/linkParaPerfil)
* **Fulano De Tal** - *Documentação* - [fulanodetal](https://github.com/linkParaPerfil)

Você também pode ver a lista de todos os [colaboradores](https://github.com/usuario/projeto/colaboradores) que participaram deste projeto.

## 📄 Licença

Este projeto está sob a licença (sua licença) - veja o arquivo [LICENSE.md](https://github.com/usuario/projeto/licenca) para detalhes.

## 🎁 Expressões de gratidão

* Conte a outras pessoas sobre este projeto 📢
* Convide alguém da equipe para uma cerveja 🍺 
* Obrigado publicamente 🤓.
* etc.


---
⌨️ com ❤️ por [Rodrigo Camargo]() 😊