<template>
  <form id="product-form" @submit.prevent="createProduct">
    <span>Cadastrar Produto</span>
    <div class="input-container">
      <label for="description">Descrição </label>
      <input
        class="text"
        type="text"
        id="description"
        name="description"
        placeholder="Informe a descrição do produto"
        v-model="description"
      />
      <p
        class="error"
        v-for="error of v$.description.$errors"
        :key="error.$uid"
      >
        {{ error.$message }}
      </p>
    </div>
    <div class="input-container">
      <label for="category">Categoria </label>
      <select name="category" id="category" class="text" v-model="category">
        <option value="Categoria A">Categoria A</option>
        <option value="Categoria B">Categoria B</option>
        <option value="Categoria C">Categoria C</option>
      </select>

      <p class="error" v-for="error of v$.category.$errors" :key="error.$uid">
        {{ error.$message }}
      </p>
    </div>
    <div class="input-container">
      <label for="un">Unidade de Medida </label>
      <select name="un" id="un" class="text" v-model="un">
        <option value="Unidade">Unidade</option>
        <option value="Metro">Metro</option>
        <option value="kilo">Kilo</option>
      </select>
      <p class="error" v-for="error of v$.un.$errors" :key="error.$uid">
        {{ error.$message }}
      </p>
    </div>
    <div class="input-container">
      <label for="storage">Estoque </label>
      <input
        class="text"
        type="text"
        id="storage"
        name="storage"
        v-model="storage"
        placeholder="Informe a quantidade em estoque"
      />

      <p class="error" v-for="error of v$.storage.$errors" :key="error.$uid">
        {{ error.$message }}
      </p>
    </div>
    <div class="input-container">
      <label for="price">Valor </label>
      <input
        class="text"
        type="text"
        id="price"
        name="price"
        v-model="price"
        placeholder="Informe o valor do produto"
      />
      <p class="error" v-for="error of v$.price.$errors" :key="error.$uid">
        {{ error.$message }}
      </p>
    </div>
    <div class="check">
      <input
        class="checkbox"
        type="checkbox"
        name="destaque"
        v-model="destaque"
        value="destaque"
      />
      <label for="destaque">Em Destaque?</label>
    </div>
    <input type="submit" class="submit-btn" value="Cadastrar" />
  </form>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { helpers, numeric, required } from "@vuelidate/validators";

export default {
  name: "NewProductForm",

  data() {
    return {
      v$: useVuelidate(),
      description: null,
      category: null,
      un: null,
      storage: null,
      price: null,
      destaque: null,
    };
  },
  validations() {
    return {
      description: {
        required: helpers.withMessage("Descrição é obrigatório", required),
        $autoDirty: true,
        $invalid: true,
      },
      category: {
        required: helpers.withMessage("Categoria é obrigatório", required),
        $autoDirty: true,
      },
      un: {
        required: helpers.withMessage(
          "Unidade de Medida é obrigatório",
          required
        ),
        $autoDirty: true,
      },
      storage: {
        required: helpers.withMessage(
          "Quantidade em estoque é obrigatório",
          required
        ),
        numeric: helpers.withMessage(
          "Um valor numérico é obrigatório",
          numeric
        ),
        $autoDirty: true,
      },
      price: {
        required: helpers.withMessage("Preço é obrigatório", required),
        numeric: helpers.withMessage(
          "Um valor numérico é obrigatório",
          numeric
        ),
        $autoDirty: true,
      },
    };
  },

  methods: {
    async createProduct(e) {
      e.preventDefault();
      if (
        this.description != null &&
        this.description != "" &&
        this.category != null &&
        this.category != "" &&
        this.un != null &&
        this.un != "" &&
        this.storage != null &&
        this.storage != "" &&
        this.price != null &&
        this.price != ""
      ) {
        console.log(this.description);

        const data = {
          description: this.description,
          category: this.category,
          un: this.un,
          storage: this.storage,
          price: this.price,
          destaque: this.destaque,
        };
        const dataJson = JSON.stringify(data);
        const req = await fetch("http://localhost:3000/products", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: dataJson,
        });
        const res = await req.json();
        alert("Cadastro realizado com sucesso");
      } else {
        alert("Você precisa preencher todos os campos");
      }
    },
  },

  submit(e) {
    this.$v.$touch();
  },
};
</script>

<style scoped>
span {
  font-weight: 400;
  font-size: 1.25rem;
}
#product-form {
  display: flex;
  flex-direction: column;
  padding: 2rem;
  gap: 1rem;

  position: absolute;
  width: 800px;
  height: auto;
  left: 256px;
  top: 71px;

  background: #ffffff;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.15);
  border-radius: 8px;
}
.input-container {
  display: flex;
  flex-direction: column;
}
.text {
  background: #f5f5f5;
  border: 1px solid #d9d9d9;
  color: #7b7b7b;
  width: 320px;
  height: 1.8rem;
  padding: 0;
  font-size: 0.9rem;
  font-weight: 400;
  padding: 0 0.5rem;
}
.input-container label {
  font-size: 0.8rem;
  color: #000000;
  padding: 0.2rem;
}
#description {
  width: 680px;
}

.ckeck {
  flex: row;
}
.checkbox {
  min-width: 23px;
  min-height: 23px;
  margin-right: 5px;
}
.submit-btn {
  width: 101px;
  height: 31px;

  background: #214171;
  border-radius: 8px;
  border: none;

  color: #ffffff;
  font-size: 0.8rem;
  font-weight: 700;
  cursor: pointer;
}

.submit-btn:hover {
  background: #061a36;
}
p {
  font-size: 0.8rem;
  margin: 3px;
  color: red;
}
</style>
