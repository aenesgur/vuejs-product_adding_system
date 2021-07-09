<template>
  <div class="row">
    <div class="card offset-2 col-md-3">
      <div class="card-body tex-center d-flex align-items-center flex-column">
        <img
          height="128"
          class="img-responsive text-center mb-3"
          :src="
            product.selectedImage == null
              ? '/src/assets/default.png'
              : product.selectedImage
          "
        />
        <input
          ref="file"
          type="file"
          style="display: none"
          @change="onChange($event)"
          class="form-control"
        />
        <button
          class="btn btn-outline-secondary"
          type="button"
          @click="$refs.file.click()"
        >
          Choose a picture
        </button>
      </div>
    </div>
    <div class="col-md-5">
      <div class="col-md-11 card">
        <div class="card-body">
          <div class="form-group">
            <label>Product Name</label>
            <input
              v-model="product.title"
              type="text"
              class="form-control"
              placeholder="Ex: Pen"
            />
          </div>
          <div class="row">
            <div class="form-group col-md-6">
              <label>Product Count</label>
              <input
                v-model="product.count"
                type="number"
                class="form-control"
                placeholder="Ex: 3"
              />
            </div>
            <div class="form-group col-md-6">
              <label>Product Price</label>
              <input
                v-model="product.price"
                type="number"
                class="form-control"
                placeholder="Ex: 100"
              />
            </div>
          </div>
          <button @click="addProduct" class="btn btn-outline-info btn-block">
            Add!
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {eventBus} from '../main'
export default {
  data() {
    return {
      product: {
        selectedImage: null,
        title: null,
        count: null,
        price: null,
        totalPrice: null,
      },
    };
  },
  methods: {
    onChange(e) {
      const file = e.target.files[0];
      this.product.selectedImage = URL.createObjectURL(file);
    },
    addProduct() {
      this.product.totalPrice = this.product.count * this.product.price;
      eventBus.$emit('productAdded', this.product);
      this.product = {
        selectedImage: null,
        title: null,
        count: null,
        price: null,
        totalPrice: null,
      }
    },
  },
};
</script>
