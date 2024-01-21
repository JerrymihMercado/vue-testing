<template>
  <div class="container-fluid">
    <h1 class="text-primary">hello</h1>

<div class="">
  
<form @submit.prevent="AddProduct">
<input
   id="text" v-model="text">
  <button type="submit" style="padding:10px 20px" >Submit </button>
</form>

  <p v-for="product in products" :key="product.id">
  {{ product.title }}
</p>

</div>

<div class="">
  
<form @submit.prevent="editProduct">
<input
   id="text" v-model="product.title">
  <button type="submit" style="padding:10px 20px" >Edit </button>
</form>

  <p v-for="product in products" :key="product.id">
  {{ product.title }}
</p>

</div>
<button type="button" style="padding:10px 20px" @click="deleteProduct"  >Delete </button>
  </div>
</template>

<script setup>
import axios from "axios";
import { watch,ref, onMounted   } from "vue";
const products = ref([]);
const text = ref("");
const product = ref({title:""});


const getAllProduct = () => {
  axios({
    method: "get",
    url: "https://dummyjson.com/products/",
   
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
  e.preventDefault()
  console.log("Add")
  axios({
    method: "post",
    url: "https://dummyjson.com/products/add",
    data: {
      title: text.value,
    },
  })
    .then((data) => {
      console.log(data);
    })
    .catch((err) => {
      console.log(err);
    });
};


const editProduct = (e) => {
  e.preventDefault()
  console.log("edit")
  axios({
    method: "PUT",
    url: "https://dummyjson.com/products/1",
    data: {
      title: product.value.title
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
  e.preventDefault()
  console.log("delete")
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
      console.log("ret",data.data);
      product.value = data.data;
    })
    .catch((err) => {
      console.log(err);
    });
};
watch(() => {
  // getAllProduct();
});
onMounted(()=>{
   getSingleProduct()
})
</script>

<style></style>
