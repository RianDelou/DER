# Banco de Dados 

<h1>Objetivo: Desenvolver um diagrama entidade relacionamento para um sistema de gestão de vendas online, de acordo com os requisitos mínimos do professor</h1>

<h2>
  <p>Estudante: Rian Lima Delou</p>
  <p>Tema: Sistema de Gestão de Vendas Online</p>
</h2>

<h3> Explicando a minha lógica para esse projeto 
<p>recomendo a leitura com a visualização do diagrama</p>
</h3>


<p>Primeiramente, criei a entidade <b>cliente</b> com os seguintes atributos: nomeCliente (Um atributo simples), telefone (Um atributo multivalorado, pois o cliente pode ter vários telefones), idade (atributo simples), e-mail (atributo simples) e <b>senha (atributo chave)</b></p>
<p>Além disso, a entidade cliente ela é uma superclasse, possuindo dois subtipos: <b>pessoa_física</b> e <b>pessoa_juridica</b>. Ou seja, ela possui uma especialização para esses dois subtipos. A pessoa juridica vai ter um benefício que irei citar posteriormente.</p>
<p>Com isso, as subclasses pessoa física e pessoa juridica possui os seguintes atributos, respectivamente: CPF (atributo simples), RG(atributo simples) e o <b>idPessoaFísica (atributo chave)</b>. CNPJ (atributo simples), IE (atributo simples), IM (atributo simples) e <b>idPessoaJuridica (atributo chave)</b> Esses atributos criados para esses dois subtipos são feitos justamente para identificação do mesmo.</p>
<p>A entidade cliente tem uma relação chamada "apresenta" que interliga {cliente && endereço}. A lógica dessa relação seria a seguinte: o cliente deve apresentar o endereço, no qual seria o endereço de entrega dos produtos. Cliente apresenta um endereço, endereço é apresentado por um cliente. Cardinalidade: 1:1</p>
<p>Os atributos da entidade <b>endereço</b> seriam: CEP(atributo simples), rua(atributo simples), bairro(atributo simples), num(atributo simples), complemento (atributo opcional, se o cliente não quiser colocar, não teria problema.) e <b>idEndereço(atributo chave)</b></p>
<p>finalizando a entidade cliente, temos uma outra relação nela chamada "Realiza", que interliga {cliente && pedido). A lógica dessa relação seria a seguinte: o cliente realiza pedidos, cada pedido é pra um único cliente. Cliente pode realizar um ou vários pedidos, o pedido é realizado por um cliente. Cardinalidade: 1:n</p>
<p>A entidade <b>pedido</b> é uma entidade fraca e eu irei explicar o porquê disso posteriormente. Ela possui os seguintes atributos: dataPedido(atributo simples), dataEntrega(atributo simples), metodoEnvio(atributo composto, possui dois outros atributos dentro dele, que seriam: padrão {simples} e expressa {simples}. O pedido pode ser entregue via entrega padrão ou expressa), endereço(atributo simples, o endereço é colocado no pedido), quantProdutos(atributo multivalorado, o cliente pode colocar 1 ou vários produtos) e  <b>idPedido(atributo chave)</b></p>
<p><b>Qual o motivo da entidade pedido ser fraca?</b> o motivo disso seria justamente por causa do endereço. O pedido apenas é realizado quando se tem o endereço, ou seja, <b>quando tiver a entidade endereço</b>. Por esse motivo ela é uma entidade fraca, sem a entidade endereço o pedido nunca é realizado. E o endereço deve ser apresentado pelo cliente antes do pedido ser feito. Depois de apresentado, conseguimos fazer o pedido.</p>
<p>Vamos agora falar sobre uma relação que a entidade pedido tem! ela se chama: "contém", que interliga {pedido && produto}. E essa relação ela é especial! Ela é uma: entidade associativa, pois ela não é apenas uma relação, ela é uma relação e ao mesmo tempo uma entidade!, que se chama: produto_pedido</p>
<p>Por qual motivo essa entidade associativa existe? bom, para entender isso, vamos falar sobre a cardinalidade dessa relação "contém". Como eu falei antes, essa relação interliga pedido e produto, a lógica dela seria: o pedido pode conter vários produtos e os produtos são contidos em vários pedidos. Pedido contém um ou vários produtos, produtos são contidos em 1 ou vários pedidos. Cardinalidade: <b>n:n</b> Quando temos essa cardinalidade n:n, podemos ter informações corrompidas, ou informações redundantes!</p>
<p>Quando isso acontece, temos que criar essa agregação ou entidade associativa, que é feita justamente para separar os dados individualmente e termos outro lugar para conseguir armazenar os dados de forma organizada! o nome dessa entidade associativa é: produto_pedido</p>
<p>Como qualquer outra entidade, a <b>entidade associativa produto_pedido</b> possui dois atributos: valorProdutoTotal (derivado, vou explicar por qual motivo ele é derivado depois, pois esse atributo seria a soma dos valores dos produtos) e numVendas. (não possui chave)</p>
<p>Falando agora sobre a entidade <b>produto</b> ela possui os seguintes atributos: nome (simples), descricaoProduto(simples), quantEstoque(multivalorado, pode ter um ou vários em estoque), dimensoes(composto, possui dois outros atributos dentro dela, que seriam: comprimento{simples} e largura{simples} cada produto tem sua dimensão), avaliacaoMedia(derivado e opcional, irei explicar o porquê disso depois, mas ela é uma média de avaliações, por isso é derivado é opcional, porque ela pode não ter avaliações) e <b>idProduto (chave)</b></p>
<p>A entidade produto tem uma relação chamada: "contém". Na qual interliga {produto && avaliação} A lógica dela seria: produto contém nenhuma ou muitas avaliações, a avaliação ela pertence a um único produto. Cardinalidade 1:n</p>
<p>A entidade <b>avaliação</b> possui os seguintes atributos: comentário(simples), quantEstrelas(composto, possui 5 atributos, 1, 2, 3, 4, 5 {todos simples}, eles seriam justamente a nota que vai ser dada) e o <b>idAvaliação (atributo chave)</b></p>
<p>A entidade avaliação tem relação com o atributo derivado da entidade Produto, pois a avaliação média surge justamente a partir das avaliações, ou seja, esse atributo derivado vai calcular a média da quantidade de estrelas dadas, criei outra entidade para conseguir armazenar a quantidade de estrelas dadas.</p>
<p>Falando sobre a útima relação que o produto tem, que seria: "Associado". Na qual interliga {produto && valorProduto} A lógica dela seria: produto está associado a um único valor, o valor é associado a um único produto. Cada produto tem seu único valor. Cardinalidade 1:1</p>
<p>A entidade <b>valorProduto</b> possui os seguintes atributos: custo(simples), atualizaçãoCusto(simples) e o <b>idValorProduto(chave)</b></p>
<p>Essa entidade foi criada para armazenar o valor do custo do produto e ter a sua devida atualização, pois o valor não é estatico, ele pode mudar. Além disso, o principal motivo pela criação, foi por causa do atributo derivado na entidade associativa "produto_pedido" o atributo: valorProdutototal, pois o valor tem que ter um lugar para ser armazenado e atualizado devidamente, fazendo com que a soma dele esteja armazenado nessa entidade associativa.</p>
<p>Voltando agora para a entidade <b>pedido</b>, temos uma útima relação que ele tem e podemos falar, a relação: "gera", que interliga{</p>


