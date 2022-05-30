

<template>
  <div class="container mt-3 mb-5">
    <table class="table mb-5">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Price</th>
          <th scope="col">Star</th>
          <th scope="col">Image</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="product in products"
          :key="product.id"
        >
          <td>{{product.id}}</td>
          <td>{{product.name}}</td>
          <td>{{product.price}}</td>
          <td>{{product.star}}</td>
          <td>
            <img
              style="height: 80px; width: 80px"
              class="img-thumbnail"
              :src="product.image"
              alt=""
            >
          </td>
        </tr>

      </tbody>
    </table>
    <form class="needs-validation">
      <div class="mb-3">
        <label>Id mới: {{product.id}}</label>
      </div>
      <div class="mb-3 has-validation">
        <label class="form-label">Name</label>
        <input
          type="text"
          class="form-control error text-danger"
          :value="product.name"
          @input="(e) => {onInputChange(e, 'name')}"
        >
        <div
          class="text-danger"
          v-if="error.name"
        >
          Input is required.
        </div>
      </div>
      <div class="mb-3">
        <label class="form-label">Price</label>
        <input
          type="text"
          class="form-control"
          :value="product.price"
          @input="(e) => {onInputChange(e, 'price')}"
        >
        <div
          class="text-danger"
          v-if="error.price"
        >
          Input is required.
        </div>
      </div>
      <div class="mb-3">
        <label class="form-label">Star</label>
        <input
          type="text"
          class="form-control"
          :value="product.star"
          @input="(e) => {onInputChange(e, 'star')}"
        >
        <div
          class="text-danger"
          v-if="error.star"
        >
          Input is required.
        </div>
      </div>
      <div class="mb-3">
        <label class="form-label">Image</label>
        <input
          type="text"
          class="form-control"
          :value="product.image"
          @input="(e) => {onInputChange(e, 'image')}"
        >
        <div
          class="text-danger"
          v-if="error.image"
        >
          Input is required.
        </div>
      </div>
      <button
        type="submit"
        class="btn btn-primary"
        @click="onFormSubmit"
      >Submit</button>
    </form>
  </div>
</template>

<script>
import { products } from "../data";

let id = products.length;

export default {
  data() {
    return {
      products: products,
      product: {
        id: ++id,
        name: "",
        price: "",
        star: 5,
        image: "",
      },
      error: {
        name: false,
        price: false,
        star: false,
        image: false,
      },
    };
  },
  methods: {
    onInputChange(e, field) {
      this.product[field] = e.target.value;
    },

    onFormSubmit(e) {
      e.preventDefault();
      const isValid = true;
      const fields = ["name", "price", "star", "image"];

      for (let i = 0; i < fields.length; i++) {
        if (this.product[fields[i]] === "") {
          this.error[fields[i]] = true;
          isValid = false;
          break;
        } else {
          this.error[fields[i]] = false;
        }
      }

      if (isValid) {
        this.products.push(this.product);
      }
    },
  },
};
</script>

<style>
</style>
