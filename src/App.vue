// Root component
<template>
  <!-- <myComp /> -->

  <div class="container">
    <div class="card">
      <h3>Sepet</h3>
      <ul>
        <li v-for="item in sepet" :key="item.id">{{ item.name }}</li>
      </ul>
      <p v-if="sepet.length == 0">Sepetiniz boş alışverişe hemen başlayın..</p>
    </div>
    <ProductAdd @add:product="addProduct"/>
    <Product
      @delete:product="deleteProduct"
      @update:product="updateProduct"
      @addToCard="sepet.push($event)"
      :product="product"
      v-for="product in products"
      :key="product.id"
    />
  </div>
</template>

<script>
// import MainContainer from "@/components/MainContainer"
import Product from "@/components/Product";
import ProductAdd from "@/components/productAdd"
export default {
  components: {
    Product,
    ProductAdd
    // myComp : MainContainer
    // MainContainer şeklinde doğrudan tanıtıp kendi ismiyle template arasında kullanabiliriz.
  },
  data() {
    return {
      products: [],
      sepet: [],
    };
  },
  mounted(){
    this.getProducts();
  },
  methods: {
    async getProducts(){
      const result = await fetch("http://localhost:3000/products")
      const data = await result.json();
      this.products = data;
    },
    async deleteProduct(product) {
      await fetch('http://localhost:3000/products/'+product.id,{
        method:"DELETE"
      })
      this.products = this.products.filter(
        (productToFilter) => productToFilter.id !== product.id
      );
      // yukarıdaki filtreleme işlemi yerine tekrar get fonksiyonunu da çağırabiliriz
    },
    async updateProduct(product) {
      const result = await fetch('http://localhost:3000/products/'+product.id,{
        method:"PUT",
        body:JSON.stringify(product),
        headers:{"Content-Type":"application/json"}
      })
      const updatedProduct = await result.json();
      this.products = this.products.map(product => product.id === updatedProduct.id?updatedProduct:product)

    },
    async addProduct(product){
      const result = await fetch('http://localhost:3000/products',{
        method:"POST",
        body:JSON.stringify(product),
        headers:{"Content-Type":"application/json"}
      })

      // const newProduct = {...product} // yeni referans alıyoruz. // httpden önce yapıldı.
      const newProduct = await result.json();
      this.products = [...this.products,newProduct]
    }
  },
};
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
</style>
