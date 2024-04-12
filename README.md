# Banco de Dados 

<h1>Objetivo: Desenvolver um diagrama entidade relacionamento para um sistema de gestão de vendas online, de acordo com os requisitos mínimos do professor</h1>

<h2>
  <p>Estudante: Rian Lima Delou</p>
  <p>Tema: Sistema de Gestão de Vendas Online</p>
</h2>

<h3>Mudanças que fiz (os parágrafos em strong são as análises do professor): </h3>
<p><b>como saber qual o valorProduto está associado a qual produto?</b></p>
<p>Para solucionar esse problema, eu analisei a entidade: "valorProduto" e percebi que poderia agrupar ela com a entidade produto. Foi isso que fiz! transformei a entidade valorProduto em um atributo da entidade produto: atributo simples "valor".</p>
<p><b>A notação clássica está misturada com a mín-máx.</b></p>
<p>Para solucionar isso, tirei todas as entidades fracas.</p>
<p><b>Várias entidades poderiam ser agrupadas.</b></p>
<p>Para solucionar isso, agrupei muitas entidades! como: endereço, valorProduto, e pagamento. Fiz o agrupamento delas pelo fato de sua cardinalidade no relacionamento ser (1,1), desse jeito eu preciso transformar em atributo, para o diagrama ficar mais tranquilo de manipular na linguagem de consulta (SQL)</p>
<p><b>Telefone (entidade fraca) precisa de um cliente (entidade forte), mas endereço não precisa (você colocou como entidade forte) e ao mesno tempo cardinalidade mín igual a 1 (indicando entidade fraca ou dependente da existência de outra entidade para ser cadastrada na base).</b></p>
<p>Para solucionar isso, eu removi a entidade endereço! fiz a remoção pelo fato de ser (1,1), pois cada cliente tem seu próprio endereço, seu próprio apartamento... Além de que na minha lógica ela não pode ter cardinalidade (0,1), pois como que eu irei realizar o pedido, sem ter o endereço do usuário? então ela deve ser obrigatória.</p>

<h3> Explicando a minha lógica para esse projeto 
<p>{recomendo a leitura com a visualização do diagrama}</p>
</h3>


<p>Primeiramente, criei a entidade <b>cliente</b> com os seguintes atributos: nomeCliente (Um atributo simples), idade (atributo simples), e-mail (atributo simples), endereço (atributo composto que possui vários atributos simples, como: CEP, Rua, Bairro, NumAp) e <b>senha (atributo chave)</b></p>
<p>Além disso, a entidade cliente ela é uma superclasse, possuindo dois subtipos: <b>pessoa_física</b> e <b>pessoa_juridica</b>. Ou seja, ela possui uma especialização para esses dois subtipos. A pessoa juridica vai ter um benefício que irei citar posteriormente.</p>
<p>Com isso, as subclasses pessoa física e pessoa juridica possui os seguintes atributos, respectivamente: CPF (atributo simples), RG(atributo simples) e o <b>idPessoaFísica (atributo chave)</b>. CNPJ (atributo simples), IE (atributo simples), IM (atributo simples) e <b>idPessoaJuridica (atributo chave)</b>.
<p>entidade cliente Possui um relacionamento "inclui" que interliga {cliente && telefoneCliente<b>(entidade fraca)</b>}. A lógica dessa relação seria que: o cliente pode incluir NENHUM, ou mais telefones, um telefone é incluido por um único cliente. Cardinalidade: 0:n. Além disso, a entidade telefoneCliente é fraca, pelo fato de ser dependente de cliente, possuindo cardinalidade (0, N) perante a ela.</p>
<p>Os atributos da entidade fraca telefone Cliente seriam: telefoneFixo(opcional), telefoneCelular(simples), telefoneAdicional(opcional), telefoneEmpresarial(simples, apenas pessoaJuridica possui esse telefone.) o <b>idTelefone(chave fraca)</b> e a chave <b> idCliente </b> telefone possui chave primaria composta!. Essa entidade é fraca pelo motivo de depender do cliente.
<p>finalizando a entidade cliente, temos uma outra relação nela chamada "Realiza", que interliga {cliente && pedido}. A lógica dessa relação seria a seguinte: o cliente realiza pedidos, cada pedido é pra um único cliente. Cliente pode realizar um ou vários pedidos, o pedido é realizado por um cliente. Cardinalidade: 1:n</p>
<p>A entidade <b>pedido</b> possui os seguintes atributos: dataPedido(atributo simples), dataEntrega(atributo simples), metodoEnvio(atributo composto, possui dois outros atributos dentro dele, que seriam: padrão {simples} e expressa {simples}. O pedido pode ser entregue via entrega padrão ou expressa), pagamento(atributo composto que possui 3 atributos simples: tipoPagamento, confirmaçãoPagamento e notaFisca) e  <b>idPedido(atributo chave)</b></p>
<p>Vamos agora falar sobre uma relação que a entidade pedido tem! ela se chama: "contém", que interliga {pedido && produto}. E essa relação ela é especial! Ela é uma: entidade associativa, pois ela não é apenas uma relação, ela é uma relação e ao mesmo tempo uma entidade!, que se chama: produto_pedido</p>
<p>Por qual motivo essa entidade associativa existe? bom, para entender isso, vamos falar sobre a cardinalidade dessa relação "contém". Como eu falei antes, essa relação interliga pedido e produto, a lógica dela seria: o pedido pode conter vários produtos e os produtos são contidos em vários pedidos. Pedido contém um ou vários produtos, produtos são contidos em 1 ou vários pedidos. Cardinalidade: <b>n:n</b> Quando temos essa cardinalidade n:n, podemos ter informações corrompidas, ou informações redundantes!</p>
<p>Quando isso acontece, temos que criar essa agregação ou entidade associativa, que é feita justamente para separar os dados individualmente e termos outro lugar para conseguir armazenar os dados de forma organizada! o nome dessa entidade associativa é: produto_pedido</p>
<p>Como qualquer outra entidade, a <b>entidade associativa produto_pedido</b> possui um atributo: valorProduto (derivado, vou explicar por qual motivo ele é derivado depois, pois esse atributo seria a soma dos valores dos produtos) (não possui chave)</p>
<p>Além disso, a entidade associativa ela é uma entidade fraca, pois ela precisa obrigatoriamente dos valores dos produtos para conseguir ser executada. Como eu irei conseguir ir ao pagamento, sem o valor total dos produtos? por isso ela é uma entidade fraca e precisa de outra entidade para existir</p> 
<p>Falando agora sobre a entidade <b>produto</b> ela possui os seguintes atributos: nome (simples), valor(simples), descricaoProduto(simples), quantEstoque(simples), dimensoes(composto, possui dois outros atributos dentro dela, que seriam: comprimento{simples} e largura{simples} cada produto tem sua dimensão), avaliacaoMedia(derivado e opcional, irei explicar o porquê disso depois, mas ela é uma média de avaliações, por isso é derivado é opcional, porque ela pode não ter avaliações) e <b>idProduto (chave)</b></p>
<p>A entidade produto tem uma relação chamada: "contém". Na qual interliga {produto && avaliação} A lógica dela seria: produto contém NENHUMA ou muitas avaliações, a avaliação ela pertence a um único produto. Cardinalidade 1:n</p>
<p>A entidade FRACA <b>avaliação</b> possui os seguintes atributos: comentário(simples), quantEstrelas(composto, possui 5 atributos, 1, 2, 3, 4, 5 {todos simples}, eles seriam justamente a nota que vai ser dada) e o <b>idAvaliação (atributo chave)</b></p>
<p>A entidade avaliação tem relação com o atributo derivado da entidade Produto, pois a avaliação média surge justamente a partir das avaliações, ou seja, esse atributo derivado vai calcular a média da quantidade de estrelas dadas, criei outra entidade para conseguir armazenar a quantidade de estrelas dadas.</p>
<p>Voltando agora para a entidade <b>pedido</b>, temos uma útima relação que ele tem e podemos falar, a relação: "Possui", que interliga{Pedido & desconto} a lógica dessa relação seria a seguinte: Pedido possui NENHUM ou vários descontos, o desconto pertence a um único pedido. Cardinalidade 1:n.</p>
<p>Agora, irei falar a entidade FRACA: <b>desconto</b>. Os atributos dessa entidade são: descontoPessoaJurídica(simples, aqui que ser pessoa jurídica faz diferença, como normalmente pedidos para empresa são caros, um desconto específico para eles seria agradável) e a <b>chave idDesconto</b>.</p>
<p>O útimo <b>relacionamento</b> que irei citar é o "aplica", que interliga {desconto && cupomDesconto}. A lógica desse relacionamento seria a seguinte: um desconto aplica apenas um cupom de desconto. O cupom de desconto é aplicado por vários descontos. Cardinalidade: n:1.
<p>Por fim, temos a entidade cupomDesconto. Ela possui como atributos: descontoPrimeiraCompra(simples), descontoAniversario(simples), descontoFreteGratis(simples), descontoComboItens(simples) e <b> idCupomDesconto (chave)</b>


