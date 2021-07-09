<template>
<div v-if="productList.length > 0">
<h3 class="text-center">Added Product List</h3>
    <hr>
    <div class="row product-container">
        <Product v-for="product in productList">
        <img
            class="card-img-top"
            :src="product.selectedImage"
            :alt="product.title"
        />
        <div class="card-body">
            <h5 class="card-title">{{product.title}}</h5>
            <small><strong>Count : </strong>{{product.count}}</small>
            <br />
            <small><strong>Price : </strong>{{product.price}}</small>
            <br />
            <small><strong>Total : </strong>{{product.totalPrice}}</small>
        </div>
        </Product>
    </div>
</div>
</template>

<script>
import {eventBus} from '../main'
import Product from "./Product.vue";

export default {
  components: {
    Product,
  },
  data(){
      return{
          productList: [],
      }
  },
  created(){
      eventBus.$on('productAdded', (product) => {
          if(this.productList.length < 2){
                this.productList.push(product)
                eventBus.$emit("progressBarUpdated", this.productList.length)
          }else {
              alert("Can not add product more than 2")
          }
          
          
      })
  }
};
</script>
