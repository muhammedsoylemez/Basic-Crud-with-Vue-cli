<template>
  <div>
    <form @submit.prevent="handleAdd">
      <!-- <div class="form-group">
        <label for="id">Id</label>
        <input type="text" v-model="product.id" class="form-control" id="id" />
      </div> -->
      <div class="form-group">
        <label for="categoryId">Kategori</label>
        <input type="text" v-model="product.categoryId" class="form-control" id="categoryId" />
      </div>
      <div class="form-group">
        <label for="name">Name</label>
        <input
          type="text" v-model="product.name" class="form-control" id="name"/>
      </div>
      <div class="form-group">
        <label for="description">Açıklama</label>
        <input type="text" v-model="product.description" class="form-control" id="description" />
      </div>
      <div class="form-group">
        <label for="price">Fiyat</label>
        <input type="text" v-model="product.price" class="form-control" id="price" />
      </div>
      <div class="form-group">
        <label for="quantity">Adet</label>
        <input type="text" v-model="product.quantity" class="form-control" id="quantity" />
      </div>
      <button class="btn btn-sm btn-dark" type="submit">Ekle</button>
    </form>
  </div>
</template>
<script>
export default {
    name:"product-add",
    data(){
        return{
            product:{id:'',categoryId:'',name:'',quantity:'',price:'',description:''}
        }
    },
    methods:{
        handleAdd(){
            this.$emit("add:product",this.product);
        }
    }
};
</script>
<style>

</style>
