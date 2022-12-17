<template>
  <div class="home">
    <TitlePage :title="titlePage" />
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
      value: "",
      image_src: ImagemClient,
      image_name: "Clientes",
      text_product: "Produtos Cadastrados",
      value_product: "",
      image_src_product: ImagemProduct,
      image_name_product: "Produtos",
      text_list: "Listagem de Produtos em Destaque",
    };
  },
  async mounted() {
    const req_products = await fetch("http://localhost:3000/products");
    const data_products = await req_products.json();

    this.value_product = data_products.length;

    const req_clients = await fetch("http://localhost:3000/clients");
    const data_clients = await req_clients.json();

    this.value = data_clients.length;
  },
};
</script>

<style scoped>
.card_product {
  display: flex;
  margin-top: -10rem;
  margin-left: 42rem;
}

h1 {
  margin-left: 60rem;
}
</style>
