<!-- <template>
  <div>
    <h1 class="font-bold text-center text-2xl mt-10 text-black">
      Product Management
    </h1>
    <div class="border-black border-2 m-8 p-8">
      <form class="bg-blue-300 border-black rounded-lg border-2 px-12">
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">||Add Product||</h2>
          <hr />
          <label class="pt-10 py-10" for="ProductName">Product Name:</label
          ><br />
          <input
            v-model="mydata.product.productName"
            type="text"
            ref="productName"
            id="ProductName"
            name="ProductName"
            placeholder=""
          /><br /><br />
          <label for="Price">Price:</label
          ><br />
          <input
            v-model="mydata.product.price"
            type="number"
            ref="price"
            id="Price"
            name="Price"
            placeholder=""
          /><br /><br />
          <label for="Stock">Stock:</label>
          <select
            v-model="mydata.product.stock"
            class="p-1"
            name="Stock"
            id="Stock"
            ref="stock"
          >
            <option value="Available" selected>Available</option>
            <option value="Out of Stock ">Out of Stock</option></select
          ><br /><br />
          <label for="Size">Size:</label>
          <select
            v-model="mydata.product.size"
            class="p-1"
            name="Size"
            id="Size"
            ref="size"
          >
            <option value="S">S</option>
            <option value="M" selected>M</option>
            <option value="L">L</option>
            <option value="XL">XL</option></select>
          <br /><br />
          
          <div class="mt-10">
            <button
              class="py-1 px-5 mr-5 bg-black hover:bgblack text-white font-bold text-center rounded-md mb-3"
              type="button"
              @click="onFormSubmit1()"
            >
              Add Product
            </button>
            <button
              class="py-1 px-5 bg-black hover:bgblack text-white font-bold text-center rounded-md mb-3"
              type="reset"
            >
              Reset
            </button>
          </div>
        </table>
      </form>
    </div>
    <div class="border-black border-2 m-8 p-8">
      <table class="list">
        <tr>
          <th class="px-4 border-black rounded-lg border-4">ProductId</th>
          <th class="px-4 border-black rounded-lg border-4">ProductName</th>
          <th class="px-4 border-black rounded-lg border-4">Price</th>
          <th class="px-4 border-black rounded-lg border-4">Stock</th>
          <th class="px-4 border-black rounded-lg border-4">Size</th>
          <th class="px-4 border-black rounded-lg border-4">Action</th>
        </tr>
        <tr v-for="item in mydata.allProduct" :key="item.id">
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.id }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.productName }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.price }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.stock }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.size }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.Action }}
            <button
              class="mx-3 rounded-lg bg-red-600 hover:bg-red-700 text-white w-20"
              @click="onDeleteOfProduct(item.id)"
            >
              Delete
            </button>
            <button
              class="mx-3 rounded-lg bg-green-600 hover:bg-green-600 text-white w-20"
              @click="editProduct(item.id)"
            >
              Edit
            </button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script setup lang="ts">
const mydata = reactive({
  allProduct: [],
  product: {
    productName: "",
    price: "",
    stock: "",
    size: "",
  },
});
getProductAPI();
// GET API
async function getProductAPI() {
  mydata.allProduct = await $fetch("http://localhost:3002/product/allData");
}
// POST API
async function onFormSubmit1() {
  console.log(mydata.product);
  await $fetch("http://localhost:3002/product", {
    method: "POST",
    body: JSON.stringify(mydata.product),
  });
  getProductAPI();
}
// PATCH API
async function editProduct(id) {
  console.log("console from patch api");
  let productEdit = mydata.allProduct.filter((product) => {
    if ((product.id == id)) {
      mydata.product.id = product.id;
      mydata.product.productName = product.productName;
      mydata.product.price = product.price;
      mydata.product.stock = product.stock;
      mydata.product.size = product.size;
      console.log("patch api");
    }
  });
  console.log(productEdit);
  const response = await $fetch("http://localhost:3002/product/" + id, {
    method: "PATCH",
    body: JSON.stringify(mydata.product),
  });
  getProductAPI();
}
// // Delete API
async function onDeleteOfProduct(id: string) {
  await $fetch("http://localhost:3002/product/" + id, {
    method: "DELETE",
  });
  getProductAPI();
}
</script> -->


<template>
  <div>
    <h1 class="font-bold text-center text-2xl mt-10 text-black">
      Product Management
    </h1>
    <div class="border-black border-2 m-8 p-8">
      <form
        @submit.prevent="onFormSubmit1()"
        class="bg-blue-300 border-black rounded-lg border-2 px-12"
      >
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">||Add Product||</h2>
          <hr />
          <label class="pt-10 py-10" for="ProductName">Product Name:</label
          ><br />
          <input
            v-model="mydata.product.productName"
            type="text"
            ref="productName"
            id="ProductName"
            name="ProductName"
            placeholder=""
          />
          <span
            v-for="error in v$.productName.$errors"
            :key="error.$uid"
            class="text-red-600"
            >{{ error.$message }}
          </span>
          <br /><br />
          <label for="Price">Price:</label
          ><br />
          <input
            v-model="mydata.product.price"
            type="number"
            ref="price"
            id="Price"
            name="Price"
            placeholder=""
          />
          <span
            v-for="error in v$.price.$errors"
            :key="error.$uid"
            class="text-red-600"
            >{{ error.$message }} </span
          ><br /><br />
          <label for="Stock">Stock:</label>
          <select
            v-model="mydata.product.stock"
            class="p-1"
            name="Stock"
            id="Stock"
            ref="stock"
          >
            <option value="Available" selected>Available</option>
            <option value="OutOfStock">Out of Stock</option>
          </select>
          <span
            v-for="error in v$.stock.$errors"
            :key="error.$uid"
            class="text-red-600"
            >{{ error.$message }} </span
          ><br /><br />
          <label for="Size">Size:</label>
          <select
            v-model="mydata.product.size"
            class="p-1"
            name="Size"
            id="Size"
            ref="size"
          >
            <!-- <option value="XS">XS</option> -->
            <option value="S">S</option>
            <option value="M" selected>M</option>
            <option value="L">L</option>
            <option value="XL">XL</option>
          </select>
          <span
            v-for="error in v$.size.$errors"
            :key="error.$uid"
            class="text-red-600"
            >{{ error.$message }} </span
          ><br /><br />
          <div class="mt-10">
            <button
              class="py-1 px-5 mr-5 bg-black hover:bgblack text-white font-bold text-center rounded-md mb-3"
              type="submit"
            >
              Add Product
            </button>
            <button
              class="py-1 px-5 bg-black hover:bgblack text-white font-bold text-center rounded-md mb-3"
              type="reset"
            >
              Reset
            </button>
          </div>
        </table>
        <span v-for="error in v$.$errors" :key="error.$uid"
          >{{ error.$property }}----{{ error.$message }}</span
        >
      </form>
    </div>
    <div class="border-black border-2 m-8 p-8">
      <table class="list">
        <tr>
          <th class="px-4 border-black rounded-lg border-4">ProductId</th>
          <th class="px-4 border-black rounded-lg border-4">ProductName</th>
          <th class="px-4 border-black rounded-lg border-4">Price</th>
          <th class="px-4 border-black rounded-lg border-4">Stock</th>
          <th class="px-4 border-black rounded-lg border-4">Size</th>
          <th class="px-4 border-black rounded-lg border-4">Action</th>
        </tr>
        <tr v-for="item in mydata.allProduct" :key="item.id">
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.id }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.productName }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.price }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.stock }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.size }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.Action }}
            <button
              class="mx-3 rounded-lg bg-red-600 hover:bg-red-700 text-white w-20"
              @click="onDeleteOfProduct(item.id)"
            >
              Delete
            </button>
            <button
              type="submit"
              class="mx-3 rounded-lg bg-green-600 hover:bg-green-600 text-white w-20"
              @click="editProduct(item.id)"
            >
              Edit
            </button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script setup lang="ts">
import useVuelidate from "@vuelidate/core";
import { maxLength, minLength, required } from "@vuelidate/validators";

const mydata = reactive({
  allProduct: [],
  product: {
    productName: "",
    price: "",
    stock: "",
    size: "",
  },
});

const rules = computed(() => {
  return {
    productName: {
      required,
      minLenght: minLength(5),
      maxLength: maxLength(15),
    },
    price: { required, maxLength: maxLength(9) },
    stock: { required },
    size: { required },
  };
});
const v$ = useVuelidate(rules, mydata.product);

getProductAPI();

// GET API
async function getProductAPI() {
  mydata.allProduct = await $fetch("http://localhost:3002/product/allData");
}

//POST API
async function onFormSubmit1() {
  try {
    console.log(mydata.product);
    const result = await v$.value.$validate();
    if (result) {
      alert("product created");
    } else {
      alert("product not created");
    }
    await $fetch("http://localhost:3002/product/", {
      method: "POST",
      body: JSON.stringify(mydata.product),
    });
    console.log("hello vikas");
  } catch (err) {
    // document.write();
    console.log({
      statusCode: 404,
      message: "User not found",
    });
  }
  getProductAPI();
}
// Patch API
async function editProduct(id) {
  console.log("top console from patch api");
  let productEdit = mydata.allProduct.filter((product) => {
    if ((product.id = id)) {
      mydata.product.id = product.id;
      mydata.product.productName = product.productName;
      mydata.product.price = product.price;
      mydata.product.stock = product.stock;
      mydata.product.size = product.size;
      return product;
      console.log("patch api");
    }
  });
  console.log(productEdit);
  const response = await $fetch("http://localhost:3002/product/" + id, {
    method: "PATCH",
    body: JSON.stringify(mydata.product),
  });
  getProductAPI();
}
getProductAPI();

// // Delete API
async function onDeleteOfProduct(id) {
  await $fetch("http://localhost:3002/product/" + id, {
    method: "DELETE",
  });
  getProductAPI();
}
</script>