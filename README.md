# Banco de Dados 

<h1>Objetivo: Desenvolver um diagrama entidade relacionamento para um sistema de gestão de vendas online, de acordo com os requisitos mínimos do professor</h1>

<h2>
  <p>Estudante: Rian Lima Delou</p>
  <p>Tema: Sistema de Gestão de Vendas Online</p>
</h2>

<h3>Mudanças que fiz (os parágrafos em strong são as análises do professor): </h3>h3>
<p><b>como saber qual o valorProduto está associado a qual produto?</b></p>
<p>Para isso, criei uma outra chave para o valorProduto, que seria o idProduto. Isso faz com que o valor do produto tenha uma relação direta com o produto, conseguindo ter acesso a cada produto e armazenando os valores para cada um. Porém, percebi que valorProduto é na verdade uma entidade fraca! então alterei para ela ser uma entidade fraca.</p>
<p><b>A notação clássica está misturada com a mín-máx.</b></p>
<p>Não alterei a notação, pois ela pode ser considerada tanto assim: (1,n) (1,1), quanto o inverso: (1,1) (1,n)</p>
<p><b>Várias entidades poderiam ser agrupadas.</b></p>
<p>Não alterei nada em relação a isso.</p>
<p><b>Telefone (entidade fraca) precisa de um cliente (entidade forte), mas endereço não precisa (você colocou como entidade forte) e ao mesno tempo cardinalidade mín igual a 1 (indicando entidade fraca ou dependente da existência de outra entidade para ser cadastrada na base).</b></p>
<p> Para solucionar o problema da entidade endereço, fiz com que ela virasse uma entidade fraca, para seguir a mesma lógica da entidade telefoneCliente. Depois disso, pensei na primeira análise que o professor fez: <b>como saber qual o valorProduto está associado a qual produto? </b> então, como eu posso saber qual endereço está associada a qual cliente? para solucionar isso, fiz a mesma lógica que apliquei na entidade valorProduto, fiz outra chave para a entidade endereço: idCliente. Com isso, conseguimos ter acesso a cada cliente e armazenar o endereço para cada um dos clientes. Além disso, fiz a mesma coisa para a entidade telefone cliente! </p>
<p>Finalizando, retirei o atributo "endereço" do pedido, pois o endereço tem que ser apresentado pelo cliente, ou seja, não precisamos apresentar novamente para efetuar o pedido.</p>


<h3> Explicando a minha lógica para esse projeto 
<p>{recomendo a leitura com a visualização do diagrama}</p>
</h3>


<p>Primeiramente, criei a entidade <b>cliente</b> com os seguintes atributos: nomeCliente (Um atributo simples), idade (atributo simples), e-mail (atributo simples) e <b>senha (atributo chave)</b></p>
<p>Além disso, a entidade cliente ela é uma superclasse, possuindo dois subtipos: <b>pessoa_física</b> e <b>pessoa_juridica</b>. Ou seja, ela possui uma especialização para esses dois subtipos. A pessoa juridica vai ter um benefício que irei citar posteriormente.</p>
<p>Com isso, as subclasses pessoa física e pessoa juridica possui os seguintes atributos, respectivamente: CPF (atributo simples), RG(atributo simples) e o <b>idPessoaFísica (atributo chave)</b>. CNPJ (atributo simples), IE (atributo simples), IM (atributo simples) e <b>idPessoaJuridica (atributo chave)</b>.
<p>A entidade cliente tem uma relação <b>fraca</b> chamada "apresenta" que interliga {cliente && endereço (entidade fraca)}. A lógica dessa relação seria a seguinte: o cliente deve apresentar o endereço, no qual seria o endereço de entrega dos produtos. Cliente apresenta um endereço, endereço é apresentado por um cliente. Cardinalidade: 1:1</p>
<p>Os atributos da entidade fraca <b>endereço</b> seriam: CEP(atributo simples), rua(atributo simples), bairro(atributo simples), num(atributo simples), complemento (atributo opcional, se o cliente não quiser colocar, não teria problema.), <b>idEndereço( chave fraca)</b> e a chave<b>idCliente</b> Endereço possui chave primaria composta!</p>
<p>Outro relacionamento que a entidade cliente tem, é a relação <b>fraca</b> "inclui" que interliga {cliente && telefoneCliente<b>(entidade fraca)</b>}. A lógica dessa relação seria que: o cliente pode incluir 1, ou mais telefones, um telefone é incluido por um único cliente. Cardinalidade: 1:n. Além disso, essa relação é fraca, pois ela está relacionado a sua entidade forte, na qual é dependente dela.</p>
<p>Os atributos da entidade fraca telefone Cliente seriam: telefoneFixo(opcional), telefoneCelular(simples), telefoneAdicional(opcional), telefoneEmpresarial(simples, apenas pessoaJuridica possui esse telefone.) o <b>idTelefone(chave fraca)</b> e a chave <b> idCliente </b> telefone possui chave primaria composta!. Essa entidade é fraca pelo motivo de depender do cliente.
<p>finalizando a entidade cliente, temos uma outra relação nela chamada "Realiza", que interliga {cliente && pedido}. A lógica dessa relação seria a seguinte: o cliente realiza pedidos, cada pedido é pra um único cliente. Cliente pode realizar um ou vários pedidos, o pedido é realizado por um cliente. Cardinalidade: 1:n</p>
<p>A entidade <b>pedido</b> possui os seguintes atributos: dataPedido(atributo simples), dataEntrega(atributo simples), metodoEnvio(atributo composto, possui dois outros atributos dentro dele, que seriam: padrão {simples} e expressa {simples}. O pedido pode ser entregue via entrega padrão ou expressa), quantProdutos(atributo simples) e  <b>idPedido(atributo chave)</b></p>
<p>Vamos agora falar sobre uma relação que a entidade pedido tem! ela se chama: "contém", que interliga {pedido && produto}. E essa relação ela é especial! Ela é uma: entidade associativa, pois ela não é apenas uma relação, ela é uma relação e ao mesmo tempo uma entidade!, que se chama: produto_pedido</p>
<p>Por qual motivo essa entidade associativa existe? bom, para entender isso, vamos falar sobre a cardinalidade dessa relação "contém". Como eu falei antes, essa relação interliga pedido e produto, a lógica dela seria: o pedido pode conter vários produtos e os produtos são contidos em vários pedidos. Pedido contém um ou vários produtos, produtos são contidos em 1 ou vários pedidos. Cardinalidade: <b>n:n</b> Quando temos essa cardinalidade n:n, podemos ter informações corrompidas, ou informações redundantes!</p>
<p>Quando isso acontece, temos que criar essa agregação ou entidade associativa, que é feita justamente para separar os dados individualmente e termos outro lugar para conseguir armazenar os dados de forma organizada! o nome dessa entidade associativa é: produto_pedido</p>
<p>Como qualquer outra entidade, a <b>entidade associativa produto_pedido</b> possui um atributo: valorProduto (derivado, vou explicar por qual motivo ele é derivado depois, pois esse atributo seria a soma dos valores dos produtos) (não possui chave)</p>
<p>Além disso, a entidade associativa ela é uma entidade fraca, pois ela precisa obrigatoriamente dos valores dos produtos para conseguir ser executada. Como eu irei conseguir ir ao pagamento, sem o valor total dos produtos? por isso ela é uma entidade fraca e precisa de outra entidade para existir</p> 
<p>Falando agora sobre a entidade <b>produto</b> ela possui os seguintes atributos: nome (simples), descricaoProduto(simples), quantEstoque(simples), dimensoes(composto, possui dois outros atributos dentro dela, que seriam: comprimento{simples} e largura{simples} cada produto tem sua dimensão), avaliacaoMedia(derivado e opcional, irei explicar o porquê disso depois, mas ela é uma média de avaliações, por isso é derivado é opcional, porque ela pode não ter avaliações) e <b>idProduto (chave)</b></p>
<p>A entidade produto tem uma relação chamada: "contém". Na qual interliga {produto && avaliação} A lógica dela seria: produto contém nenhuma ou muitas avaliações, a avaliação ela pertence a um único produto. Cardinalidade 1:n</p>
<p>A entidade <b>avaliação</b> possui os seguintes atributos: comentário(simples), quantEstrelas(composto, possui 5 atributos, 1, 2, 3, 4, 5 {todos simples}, eles seriam justamente a nota que vai ser dada) e o <b>idAvaliação (atributo chave)</b></p>
<p>A entidade avaliação tem relação com o atributo derivado da entidade Produto, pois a avaliação média surge justamente a partir das avaliações, ou seja, esse atributo derivado vai calcular a média da quantidade de estrelas dadas, criei outra entidade para conseguir armazenar a quantidade de estrelas dadas.</p>
<p>Falando sobre a útima relação (fraca) que o produto tem, que seria: "Associado". Na qual interliga {produto && valorProduto} A lógica dela seria: produto está associado a um único valor, o valor é associado a um único produto. Cada produto tem seu único valor. Cardinalidade 1:1</p>
<p>A entidade fraca <b>valorProduto</b> possui os seguintes atributos: custo(simples), atualizaçãoCusto(simples), o <b>idValorProduto(chave)</b> e a chave <b>idProduto </b> valorProduto possui chave composta!, conseguimos relacionar os valores de cada produto pela chave do idProduto!</p>
<p>Essa entidade foi criada para armazenar o valor do custo do produto e ter a sua devida atualização, pois o valor não é estatico, ele pode mudar. Além disso, o principal motivo pela criação, foi por causa do atributo derivado na entidade associativa "produto_pedido" o atributo: valorProduto, pois o valor tem que ter um lugar para ser armazenado e atualizado devidamente, fazendo com que a soma desses valores esteja armazenado nessa entidade associativa.</p>
<p>Voltando agora para a entidade <b>pedido</b>, temos uma útima relação que ele tem e podemos falar, a relação: "gera", que interliga{Pedido & pagamento} a lógica dessa relação seria a seguinte: Pedido gera um único pagamento, o pagamento é gerado por um único pedido. Cardinalidade 1:1.</p>
<p>A entidade pagamento possui os seguintes atributos: tipoPagamento(simples), confirmacaoPagamento(simples), notaFiscal(simples), desconto(opcional, a pessoa pode escolher ou não um desconto), valorTotal(simples) e <b>idPagamento(chave)</b></p>
<p>Falando agora sobre o relacionamento "possui". Que interliga o {pagamento && produto}, a lógica dela seria a seguinte: um pagamento possui nenhum ou um único desconto, o desconto é possuido por um único pagamento. Cardinalidade: 1:1</p>
<p>Agora, irei falar a entidade: <b>desconto</b>. Os atributos dessa entidade são: descontoPessoaJurídica(simples, aqui que ser pessoa jurídica faz diferença, como normalmente pedidos para empresa são caros, um desconto específico para eles seria agradável) e a <b>chave idDesconto</b>.</p>
<p>O útimo <b>relacionamento fraco</b> que irei citar é o "aplica", que interliga {desconto && cupomDesconto}. A lógica desse relacionamento seria a seguinte: um desconto aplica apenas um cupom de desconto. O cupom de desconto é aplicado por vários descontos. Cardinalidade: n:1.
<p>Por fim, temos a entidade cupomDesconto, que é uma entidade fraca, pois depende de desconto para existir. Ela possui como atributos: descontoPrimeiraCompra(simples), descontoAniversario(simples), descontoFreteGratis(simples), descontoComboItens(simples) e idCupomDesconto <b>(chave fraca)</b>


