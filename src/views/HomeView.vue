<template>
  <div class="home">
    <TitlePage :title="titlePage" />
    <!-- <div id="cards"> -->
    <Card
      :textCard="text"
      :valueCard="value"
      :image="image_src"
      :alt="image_name"
    />
    <Card
      class="card_product"
      :textCard="text_product"
      :valueCard="value_product"
      :image="image_src_product"
      :alt="image_name_product"
    />
    <!-- </div> -->

    <ProductList :textList="text_list" />
  </div>
</template>

<script>
import ImagemClient from "../assets/clients.png";
import ImagemProduct from "../assets/products.png";

import Card from "../components/Card.vue";
import TitlePage from "../components/TitlePage.vue";

import ProductList from "../components/ProductsList.vue";

export default {
  components: {
    TitlePage,
    Card,
    ProductList,
  },
  data() {
    return {
      titlePage: "Dashboard",
      text: "Número de Clientes",
      value: 20,
      image_src: ImagemClient,
      image_name: "Clientes",
      text_product: "Produtos Cadastrados",
      value_product: 25,
      image_src_product: ImagemProduct,
      image_name_product: "Produtos",
      text_list: "Listagem de Produtos em Destaque",
    };
  },
};
</script>

<style scoped>
.card_product {
  display: flex;
  margin-top: -10rem;
  margin-left: 42rem;
}

/* @media (max-width: 1635px) {
  #cards {
    display: flex;
  }
} */
</style>
