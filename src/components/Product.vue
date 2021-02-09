<template>
  <div class="product">
    <input v-if="updateId === product.id" type="text" id="productName" v-model="product.name">
    <strong v-else>{{ product.name }}</strong>
    <input v-if="updateId === product.id" type="text" id="productDescription" v-model="product.description">
    <p v-else>{{ product.description }}</p>
    <input v-if="updateId === product.id" type="number" id="productPrice" v-model="product.price">
    <strong v-else>Fiyat : {{ product.price }} </strong>
    <br />
    <input v-if="updateId === product.id" type="number" id="productQuantity" v-model="product.quantity">
    <strong v-else> Adet : {{ product.quantity }}</strong>
    <hr />
    <button  v-if="updateId === null" @click="addToCard(product)">Sepete Ekle</button>
    <button v-if="updateId === null" @click="handleUpdate(product)">Güncelle</button>
    <button v-else @click="handleSave(product)">Kaydet</button>
    <button v-if="updateId === null" @click="handleDelete(product)">Ürünü Sil</button>
    <button v-else @click="updateId = null">Vazgeç</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      updateId: null,
    };
  },
  props: ["product"],
  methods: {
    addToCard(product) {
      this.$emit("addToCard", product);
    },
    handleDelete(product) {
      this.$emit("delete:product", product);
    },
    handleUpdate(product){
        this.updateId = product.id
    },
    handleSave(product){
        this.$emit("update:product",product)
        this.updateId= null;
    }
  },
};
</script>
<style>
.product {
  border: 1px dashed black;
  text-align: center;
  margin: 10px;
  padding: 10px;
  width: 300px;
  transition: border 0.5s;
}
.product:hover {
  border: 2px solid #666;
}
button {
  margin-right: 5px;
  margin-left: 5px;
}
</style>
