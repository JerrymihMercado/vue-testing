<template>
  <div class="container border py-5">
    <h2 class="text-center">Products table</h2>
    <div class="row">
      <div class="col-md-12 d-flex justify-content-end pb-5">
        <button
          class="btn btn-primary"
          data-bs-toggle="modal"
          data-bs-target="#addProductModal"
        >
          Add New Product
        </button>
      </div>
      <div class="col-md-12">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Name</th>
              <th scope="col">Price</th>
              <th scope="col">Description</th>
              <th scope="col">Delete</th>
              <th scope="col">Edit</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(product, index) in products" :key="product.id">
              <th scope="row">{{ index + 1 }}</th>
              <td>{{ product.title }}</td>
              <td>{{ product.price }}</td>
              <td>{{ product.description }}</td>
              <td><button class="btn btn-danger btn-sm">Delete</button></td>
              <td><button class="btn btn-info btn-sm">Edit</button></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- Add product modal -->
    <div
      class="modal fade"
      id="addProductModal"
      tabindex="-1"
      aria-labelledby="addProductModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <form @submit.prevent="AddProduct">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="addProductModalLabel">Add prodcut</h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <div class="modal-body">
              <div class="py-2">
                <label for="product_title">Name</label>
                <input
                  id="product_title"
                  v-model="productData.name"
                  class="form-control"
                />
              </div>
              <div class="py-2">
                <label for="product_title">Price</label>
                <input
                  id="product_title"
                  type="number"
                  v-model="productData.price"
                  class="form-control"
                />
              </div>
              <div class="py-2">
                <label for="product_description">description</label>
                <input
                  id="product_description"
                  v-model="productData.description"
                  class="form-control"
                />
              </div>
            </div>
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                data-bs-dismiss="modal"
              >
                Close
              </button>
              <button type="submit" class="btn btn-primary">Submit</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { watch, ref, onMounted } from "vue";
const products = ref([]);
const text = ref("");
const product = ref({ title: "" });
const productData = ref({ title: "", price: 0, description: "" });

const getAllProduct = () => {
  axios({
    method: "get",
    url: "https://dummyjson.com/products?limit=10",
  })
    .then((data) => {
      console.log(data.data.products);
      products.value = data.data.products;
    })
    .catch((err) => {
      console.log(err);
    });
};

const AddProduct = (e) => {
  e.preventDefault();
  console.log("Add");
  axios({
    method: "post",
    url: "https://dummyjson.com/products/add",
    data: {
      title: productData.value.name,
      price: productData.value.price,
      description: productData.value.description,
    },
  })
    .then((data) => {
      console.log(data);
      products.value = [...products.value, productData.value];
      productData.value = { title: "", price: 0, description: "" };
      // Assuming your close button has a data-bs-dismiss attribute
      var closeButton = document.querySelector(
        '#addProductModal [data-bs-dismiss="modal"]'
      );

      // Simulate clicking the close button
      if (closeButton) {
        closeButton.click();
      }
    })
    .catch((err) => {
      console.log(err);
    });
};

const editProduct = (e) => {
  e.preventDefault();
  console.log("edit");
  axios({
    method: "PUT",
    url: "https://dummyjson.com/products/1",
    data: {
      title: product.value.title,
    },
  })
    .then((data) => {
      console.log(data);
    })
    .catch((err) => {
      console.log(err);
    });
};

const deleteProduct = (e) => {
  e.preventDefault();
  console.log("delete");
  axios({
    method: "DELETE",
    url: "https://dummyjson.com/products/1",
  })
    .then((data) => {
      console.log(data);
    })
    .catch((err) => {
      console.log(err);
    });
};

const getSingleProduct = () => {
  axios({
    method: "get",
    url: "https://dummyjson.com/products/1",
  })
    .then((data) => {
      console.log("ret", data.data);
      product.value = data.data;
    })
    .catch((err) => {
      console.log(err);
    });
};

onMounted(() => {
  getAllProduct();
});
</script>

<style></style>
