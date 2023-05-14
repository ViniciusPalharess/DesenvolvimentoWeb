<script setup>
import { ref } from 'vue'

const mostrarDescricao = ref(false);
const produtoSelecionado = ref({});
let showProdutos = ref(true);

const produtos = ref([
 {
   id: 1,
   nome: 'Camiseta',
   preco: 49.9,
   imagem:
     'https://static.netshoes.com.br/produtos/camisa-flamengo-iii-2122-sn-torcedor-adidas-masculina/02/3ZP-0968-002/3ZP-0968-002_zoom1.jpg?ts=1643638170',
   descricao: 'Camisa Masculina',
   link: 'https://www.adidas.com.br/camisa-3-cr-flamengo-21-masculina/GM6495.html',
   enviar: '',
   quantidade: 0
 },
 {
   id: 2,
   nome: 'Calça',
   preco: 99.9,
   imagem:
     'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT_H2SD_gZbumHeRLyIvjDLvjzVKFpqliM17w&usqp=CAU',
   descricao: 'Calça Masculina',
   link: 'https://www.magazineluiza.com.br/calca-de-helanca-masculina-gangster-19040164/p/he8bhk7740/md/ccml/',
   enviar: '',
   quantidade: 0
 },
 {
   id: 3,
   nome: 'Meia',
   preco: 9.9,
   imagem: 'https://m.media-amazon.com/images/I/310MMzs60QL._AC_.jpg',
   descricao: 'Meia Masculina',
   link: 'https://www.amazon.com.br/Mei%C3%A3o-Infantil-Flamengo-Vermelho-Oficial/dp/B0879J4DSB',
   enviar: '',
   quantidade: 0
 },
 {
   id: 4,
   nome: 'Chuteira',
   preco: 199.9,
   imagem:
     'data:image/jpeg;base64,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',
   descricao: 'Chuteira Masculina',
   link: 'https://www.netshoes.com.br/chuteira-flamengo-futsal-futebol-de-salao-campo-indoor-oxn-oficial-licenciada-cinza-Z44-3051-010',
   enviar: '',
   quantidade: 0
 },
 {
   id: 5,
   nome: 'Boné',
   preco: 29.9,
   imagem:
     'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSou9Y9ylKVEgdmqskSdChs5Ml3jteGUtqOLA&usqp=CAU',
   descricao: 'Boné Masculino',
   link: 'https://www.dafiti.com.br/Bone-adidas-Hino-Flamengo-Branco-1776827.html',
   enviar: '',
   quantidade: 0
 },
 {
   id: 6,
   nome: 'Óculos',
   preco: 99.9,
   imagem: 'https://cdn.awsli.com.br/300x300/2488/2488896/produto/18594950811830524a1.jpg',
   descricao: 'Óculos Masculino',
   link: 'https://produto.mercadolivre.com.br/MLB-1777353531-armaco-lentes-blue-cut-proteco-a-luz-azul-com-seu-grau-_JM',
   enviar: '',
   quantidade: 0
 },
 {
   id: 7,
   nome: 'Relógio',
   preco: 299.9,
   imagem:
     'data:image/jpeg;base64,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',
   descricao: 'Relógio Masculino',
   link: 'https://produto.mercadolivre.com.br/MLB-1554877188-relogio-technos-masculino-flamengo-flagl15am4p-aco-oficial-_JM',
   enviar: '',
   quantidade: 0
 },
 {
   id: 8,
   nome: 'Bermuda',
   preco: 79.9,
   imagem:
     'https://webshop.vteximg.com.br/arquivos/ids/193634-0-0/M_0089_001004415_03.jpg?v=637510682101870000',
   descricao: 'Bermuda Masculina',
   link: 'https://www.lojabraziline.com.br/bermuda-flamengo-loot-infantil/p',
   enviar: '',
   quantidade: 0
 },
 {
   id: 9,
   nome: 'Cueca',
   preco: 19.9,
   imagem:
     'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTcm7fSSl6n8q-bCM6k0LGMUNFPlGiqMA4wwg&usqp=CAU',
   descricao: 'Cueca Masculina',
   link: 'https://www.cea.com.br/cueca-masculina-duomo-boxer-vermelho-9971386-vermelho/p',
   enviar: '',
   quantidade: 0
 },
 {
   id: 10,
   nome: 'Casaco',
   preco: 9.9,
   imagem:
     'https://flamengo.vteximg.com.br/arquivos/ids/166778-473-473/HR3113_1_APPAREL_Photography_Standard-View_white.jpg?v=638164194299800000',
   descricao: 'Casaco Masculino',
   link: 'https://loja.flamengo.com.br/moletom-flamengo-lifestyle-adidas-2023/p',
   enviar: '',
   quantidade: 0
 }
]);

const carrinhos = ref({

 items: [],
 total: 0,

});

function adicionar(produto) {
  const index = carrinhos.value.items.findIndex(item => item.id === produto.id);
  const estoque = produto.quantidade;

  if (index >= 0) {
    if (carrinhos.value.items[index].quantidade + 1 > estoque) {
      alert(`Produto já existente no carrinho`);
      return;
    }

    carrinhos.value.items[index].quantidade += 1;
    carrinhos.value.items[index].preco = carrinhos.value.items[index].quantidade * carrinhos.value.items[index].precoUnitario;
  } else {
    const item = {
      id: produto.id,
      nome: produto.nome,
      precoUnitario: produto.preco,
      quantidade: 1,
      preco: produto.preco
    };

    carrinhos.value.items.push(item);
    produto.primeiroClique = true;
  }

  const prodIndex = produtos.value.findIndex(prod => prod.id === produto.id);
  produtos.value[prodIndex].quantidade -= 1;
  carrinhos.value.total = carrinhos.value.items.reduce((acc, item) => acc + item.preco, 0);
}

function incrementarContador(produto) {
  const index = carrinhos.value.items.findIndex(item => item.id === produto.id);

  carrinhos.value.items[index].quantidade += 1;
  carrinhos.value.total += produto.precoUnitario;
}

function decrementarContador(produto) {
  const index = carrinhos.value.items.findIndex(item => item.id === produto.id);

  if (carrinhos.value.items[index].quantidade === 1) {
    const confirmar = confirm('Voce tem certeza, que deseja remover o item?');

    if (confirmar) {
      carrinhos.value.items.splice(index, 1);
      carrinhos.value.total -= produto.precoUnitario;

      const prodIndex = produtos.value.findIndex(prod => prod.id === produto.id);
      produtos.value[prodIndex].quantidade += 1;

      if (carrinhos.value.items.length === 0) {
        carrinhos.value.total = 0;
      }
    }
  } else {
    carrinhos.value.items[index].quantidade -= 1;
    carrinhos.value.total -= produto.precoUnitario;

    const prodIndex = produtos.value.findIndex(prod => prod.id === produto.id);
    produtos.value[prodIndex].quantidade += 1;
  }
}

function removerItem(item) {
  const index = carrinhos.value.items.findIndex(i => i.id === item.id);
  const produto = produtos.value.find(p => p.id === item.id);
  const quantidade = carrinhos.value.items[index].quantidade;

  carrinhos.value.total -= item.preco * quantidade;
  carrinhos.value.items.splice(index, 1);
  produto.quantidade += quantidade;
  
}

function selecionarProduto(produto) {
  if (produto.id === produtoSelecionado.value.id) {
    mostrarDescricao.value = !mostrarDescricao.value;
  } else {
    produtoSelecionado.value = produto;
    mostrarDescricao.value = true;
  }
}

function alternarCarrinho() {
  showProdutos.value = !showProdutos.value;
}

function toggleCarrinho() {
  showProdutos.value = !showProdutos.value;
}

</script>


<template>
 <main>
    <h1>COMPRAS</h1>
    <div class="fundo">
      <button class="botaoCarrinho" @click="alternarCarrinho" :class="{ 'piscando': showProdutos }">
      {{ showProdutos ? 'Carrinho' : 'Produtos' }}
      </button>
      <div>
        <div class="carrinho-container" v-if="!showProdutos">
          <div class="item" v-for="item in carrinhos.items" :key="item.id">
            <p>Item: {{ item.nome }}</p>
            <p>Preco: {{ item.preco.toLocaleString('pt-BR', {style: 'currency', currency: 'BRL'}) }}</p>
            <p>Quantidade: {{ item.quantidade }}</p>
            <button class="decrementar" @click="decrementarContador(item)">-</button>
            <button class="incrementar" @click="incrementarContador(item)">+</button>
            <button class="remover" @click="removerItem(item)">Remover</button>
            <button class="voltarprodutos" @click="toggleCarrinho">Voltar para Produtos</button>

          </div>
          <p  class="total" > Total: {{ carrinhos.total.toLocaleString('pt-BR', {style: 'currency', currency: 'BRL'}) }}</p>
        </div>
      </div>
    </div>

    <div class="produtos"  v-if="showProdutos">
      <div v-for="produto in produtos" :key="produto.id" class="card">
        <p class="title">{{ produto.nome }}</p>
        <div class="imagem"><img :src="produto.imagem"/></div>
        <p class="quantidade">Quantidade: </p>
        <button class="button-28" @click="selecionarProduto(produto)">
          {{ mostrarDescricao && produto.id === produtoSelecionado.id ? 'Ocultar Descrição' : 'Mostrar descrição' }}
        </button>
        <div class="descricao" v-if="mostrarDescricao && produto.id === produtoSelecionado.id">
          {{ produto.descricao }}
        </div>
        <div v-if="mostrarDescricao && produto.id === produtoSelecionado.id">
        <p class="preco">Preço: {{ produto.preco.toLocaleString('pt-BR', {style: 'currency', currency: 'BRL'}) }}</p>
        <button class="button-14"><a :href="produto.link" class="link">Você pode encontrar o produto tambem em:
        </a></button>
      </div>
      <button class="button-30" @click="adicionar(produto)">Adicionar</button>
    </div>
  </div>

  </main>
</template>


<style scoped>
/* Sem Classes */

main {
 align-items: center;
 flex-direction: column;
 width: 100%;
}

h1 {
 display: flex;
 justify-content: center;
 background-color: black;
 color: white;
 width: 100%;


}

a {
 color: black;
 text-decoration: none;
}

/* Carrinho */

.carrinho-container {
  display: run-in;
  margin-top: 2%;
  background-color: #fff;
  border: 2px solid #000;
  width: 100%;
}

.remover{
  display: block;
  margin-top: 1%;
}
.voltarprodutos{
  display: block;
  margin-top: 1%;
}

.item {
  border: 2px solid black;
  margin-top: 2%;
  border-radius: 20px;
  padding: 10px;
}

.total{
display: flex;
justify-content: center;
font-size: 21px;
font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

/* Produto */
.produtos {
 display: flex;
 justify-content: center;
 flex-wrap: wrap;
 width: 100%;
}

.card {
 margin: 5%;
 border: 3px solid black;
 padding: 30px;
 border-radius: 10px;
 box-shadow: rgba(0, 0, 0, 0.137) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px,
   rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px,
   rgba(0, 0, 0, 0.09) 0px -3px 5px;
 justify-content: center;
 width: 20%;
}

.card .title {
 background-color: black;
 color: white;
 text-align: center;
 font-size: 30px;
 font-weight: 800;
}

.card .imagem {
 display: flex;
 justify-content: center;
}

.card .quantidade {
 display: flex;
 justify-content: center;
 background-color: black;
 color: white;
 width: 100%;
 font-size: 21px;
 font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

.card .contador {
 display: flex;
 justify-content: center;
 margin-top: 3%;
 margin-bottom: 5%;
}

.card img {
 display: flex;
 justify-content: center;
 max-width: 200px;
 max-height: 150px;
}


.card .descricao {
 margin-top: 5%;
 font-size: 25px;
 font-weight: 800;
}


.card .preco {
 font-size: 19px;
}

/* Botões */
.botaoCarrinho {
  position: fixed;
  background-color: #fff;
  border: 2px solid #000;
  font-size: 24px;
  margin-left: 1%;
  right: 90px;
}

@keyframes piscar {
  from { opacity: 1; }
  to { opacity: 0; }
}

.piscando {
  animation: piscar 0.7s ease-in-out infinite alternate;
}


.botaoCarrinho:hover {
  background-color: #000;
  color: #fff;
}

.incrementar {
 margin-left: 1%;
 border: 1px solid black;
}

.decrementar {
 border: 1px solid black;
}

.button-14 {
 background-image: linear-gradient(#f7f8fa, #e7e9ec);
 border-color: #adb1b8 #a2a6ac #8d9096;
 border-style: solid;
 border-width: 1px;
 border-radius: 3px;
 box-shadow: rgba(255, 255, 255, .6) 0 1px 0 inset;
 box-sizing: border-box;
 color: #0f1111;
 cursor: pointer;
 display: inline-block;
 font-family: "Amazon Ember", Arial, sans-serif;
 font-size: 14px;
 height: 29px;
 font-size: 13px;
 outline: 0;
 overflow: hidden;
 padding: 0 11px;
 text-align: center;
 text-decoration: none;
 text-overflow: ellipsis;
 user-select: none;
 -webkit-user-select: none;
 touch-action: manipulation;
 white-space: nowrap;
}

.button-14:active {
 border-bottom-color: #a2a6ac;
}

.button-14:active:hover {
 border-bottom-color: #a2a6ac;
}

.button-14:hover {
 border-color: #a2a6ac #979aa1 #82858a;
}

.button-14:focus {
 border-color: #e77600;
 box-shadow: rgba(228, 121, 17, .5) 0 0 3px 2px;
 outline: 0;
}

.button-30 {
 display: flex;
 justify-content: center;
 margin-top: 10%;
 appearance: none;
 background-color: #FCFCFD;
 border-radius: 4px;
 box-shadow: rgba(45, 35, 66, 0.4) 0 2px 4px, rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #D6D6E7 0 -3px 0 inset;
 box-sizing: border-box;
 color: #36395A;
 cursor: pointer;
 display: flex;
 font-family: "JetBrains Mono", monospace;
 height: 29px;
 width: 100%;
 line-height: 1;
 list-style: none;
 overflow: hidden;
 padding-left: 16px;
 padding-right: 16px;
 position: relative;
 text-align: left;
 text-decoration: none;
 transition: box-shadow .50s, transform .50s;
 user-select: none;
 -webkit-user-select: none;
 touch-action: manipulation;
 white-space: nowrap;
 font-size: 18px;
}

.button-30:focus {
 box-shadow: #cfcfe9 0 0 0 1.5px inset, rgba(45, 35, 66, 0.4) 0 2px 4px, rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #D6D6E7 0 -3px 0 inset;
}

.button-30:hover {
 box-shadow: rgba(75, 59, 109, 0.4) 0 4px 8px, rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #D6D6E7 0 -3px 0 inset;
 transform: translateY(2px);
}

.button-30:active {
 box-shadow: #D6D6E7 0 3px 7px inset;
 transform: translateY(-2px);
}

.button-28 {
 appearance: none;
 background-color: transparent;
 border: 3px solid #1A1A1A;
 border-radius: 10px;
 box-sizing: border-box;
 color: #3B3B3B;
 cursor: pointer;
 display: inline-block;
 font-family: "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
 font-size: 16px;
 font-weight: 600;
 min-height: 40px;
 outline: none;
 padding: 16px 24px;
 text-decoration: none;
 transition: all 3s cubic-bezier(.23, 1, 0.32, 1);
 user-select: none;
 -webkit-user-select: none;
 touch-action: manipulation;
 width: 100%;
}

.button-28:disabled {
 pointer-events: none;
}

.button-28:hover {
 color: #fff;
 background-color: #1A1A1A;
 box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
 transform: translateY(-2px);
}

.button-28:active {
 box-shadow: none;
 transform: translateY(0);
}

</style>