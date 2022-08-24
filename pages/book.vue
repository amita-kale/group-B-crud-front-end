<template>
  <div>
    <h1 class="font-bold text-center text-2xl mt-10 text-black">
      Book Management
    </h1>
    <div class="border-black border-2 m-8 p-8">
      <form class="bg-blue-300 border-black rounded-lg border-2 px-12">
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">||Add Book||</h2>
          <hr />
          <label class="pt-10 py-10" for="bookName">Book Name:</label
          ><br />
          <input
            v-model="mydata.Book.book_name"
            type="text"
            ref="book_name"
            id="book_name"
            name="book_name"
            placeholder=""
          /><br /><br />
          <label for="author">Author:</label
          ><br />
          <input
            v-model="mydata.Book.author"
            type="string"
            ref="author"
            id="author"
            name="author"
            placeholder=""
          /><br /><br />
          <label for="price">price:</label>
          <input
            v-model="mydata.Book.price"
            class="p-1"
            name="price"
            id="price"
            ref="price"
          /><br /><br />

          <label for="author">ISBN:</label
          ><br />
          <input
            v-model="mydata.Book.book_isbn"
            type="string"
            ref="book_isbn"
            id="book_isbn"
            name="book_isbn"
            placeholder=""
          /><br /><br />

          <label for="Image">Upload Image</label
          ><br /><br />
          <input type="file" id="Image" name="Image" /><br /><br />
          <div class="mt-10">
            <button
              class="
                py-1
                px-5
                mr-5
                bg-black
                hover:bgblack
                text-white
                font-bold
                text-center
                rounded-md
                mb-3
              "
              type="button"
              @click="onFormSubmit1()"
            >
              Add Book
            </button>
            <button
              class="
                py-1
                px-5
                bg-black
                hover:bgblack
                text-white
                font-bold
                text-center
                rounded-md
                mb-3
              "
              type="reset"
            >
              Reset
            </button>
          </div>
        </table>
      </form>
    </div>
    <div class="border-black border-2 m-8 p-8">
      <table :item="allProduct" id="">
        <tr>
          <th class="px-4 border-black rounded-lg border-4">BookId</th>
          <th class="px-4 border-black rounded-lg border-4">bookName</th>
          <th class="px-4 border-black rounded-lg border-4">price</th>
          <th class="px-4 border-black rounded-lg border-4">author</th>

          <th class="px-4 border-black rounded-lg border-4">Image</th>
          <th class="px-4 border-black rounded-lg border-4">isbn</th>
        </tr>
        <tr v-for="item in mydata.allProduct" :key="item">
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.book_id }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.book_name }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.author }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.price }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.book_isbn }}
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            <img src="{{item.image}}" alt="" srcset="" />
          </td>
          <td class="px-4 border-black rounded-lg border-4">
            {{ item.Action }}
            <button
              class="
                mx-3
                rounded-lg
                bg-red-600
                hover:bg-red-700
                text-white
                w-20
              "
              @click="onDeleteOfProduct(item.book_id)"
            >
              Delete
            </button>
            <button
              class="
                mx-3
                rounded-lg
                bg-green-600
                hover:bg-green-600
                text-white
                w-20
              "
              @click="onClickOfEditProduct(item.id)"
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
  Book: {
    book_name: "",
    author: "",
    price: "",
    book_isbn: "",
    image: "",
  },
});
getBookAPI();
// GET API
async function getBookAPI() {
  mydata.allProduct = await $fetch("http://localhost:3001/book");
  //getBookAPI();
}
// POST API
async function onFormSubmit1() {
  console.log(mydata.Book);
  await $fetch("http://localhost:3001/book", {
    method: "POST",
    body: JSON.stringify(mydata.Book),
  });
}
//  PATCH API
async function onClickOfEditProduct(id) {
  const sampleData = {
    id: id,
    productName: "Shaktiman" + id,
    price: "ankita" + mydata.allProduct.length,
    stock: 200 + mydata.allProduct.length,
    size: "ghjgj" + mydata.allProduct.length,
    image: "91001" + mydata.allProduct.length,
  };
  // const response = await $fetch('http://localhost:3002/product/' + id, {
  //     method: 'PATCH',
  //     body: JSON.stringify(sampleData),
  // });
  // getBookAPI();
  //getBookAPI();
}
// // Delete API
async function onDeleteOfProduct(book_id) {
  await $fetch("http://localhost:3001/book/" + book_id, {
    method: "DELETE",
  });
  getProductAPI();
}
</script>









