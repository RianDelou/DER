# Banco de Dados 

<h1>Objetivo: Desenvolver um diagrama entidade relacionamento para um sistema de gestão de vendas online, de acordo com os requisitos mínimos do professor</h1>

<h2>
  <p>Estudante: Rian Lima Delou</p>
  <p>Tema: Sistema de Gestão de Vendas Online</p>
</h2>

<h3> Explicando a minha lógica para esse projeto </h3>
<p>Primeiramente, criei a entidade <b>cliente</b> com os seguintes atributos:</p>
<p>nomeCliente (Um atributo simples), telefone (Um atributo multivalorado, pois o cliente pode ter vários telefones), idade (atributo simples), e-mail (atributo simples) e <b>senha (atributo chave)</b></p>
<p>Além disso, a entidade cliente ela é uma superclasse, possuindo dois subtipos:<b>pessoa_física</b> e <b>pessoa_juridica</b>. Ou seja, ela possui uma especialização para esses dois subtipos. A pessoa juridica vai ter um benefício que irei citar posteriormente.</p>
<p>Com isso, as subclasses pessoa física e pessoa juridica possui os seguintes atributos, respectivamente: CPF (atributo simples), RG(atributo simples) e o <b>idPessoaFísica (atributo chave)</b>. CNPJ (atributo simples), IE (atributo simples), IM (atributo simples) e <b>idPessoaJuridica (atributo chave)</b></p>
<p>Esses atributos criados para esses dois subtipos são feitos justamente para identificação.</p>


