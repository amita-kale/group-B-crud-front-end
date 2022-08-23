<template>
  <div class="container mx-auto p-8">
    <h1 class="font-bold text-gray-600 text-lg text-center">Book Management</h1>
    <div class="text-center">
      <label for="search" class="font-semibold p-1">Search By Book Id</label>
      <input
        type="number"
        id="search"
        name="search"
        class="border-2 border-black m-1 rounded-lg"
      />
      <button
        class="p-1 rounded-lg bg-sky-400 border-2  border-black text-black w-20"
        @click="getspecificuser"
      >
        Search
      </button>
    </div>
    <form class="text-center" method="POST">
      <label for="fname" class="font-semibold p-1">Book:</label>
      <input
        type="number"
        id="Bid"
        name="Bid"
        placeholder=""
        class="border-2 border-black m-1"
        v-model="book.book_id"
      /><br />
      <label for="fname" class="font-semibold p-1"> Book Name:</label>
      <input
        type="text"
        id="bname"
        name="bname"
        placeholder=""
        class="border-2 border-black m-1"
        v-model="book.book_name"
      /><br />
      <label for="address" class="font-semibold p-1">Author</label>
      <input
        type="text"
        id="author"
        name="author"
        placeholder=""
        class="border-2 border-black m-1"
        v-model="book.author"
      />
      <br />
      <label for="contact" class="font-semibold p-1">price</label>
      <input
        type="number"
        id="price"
        name="price"
        placeholder=""
        class="border-2 border-black m-1"
        v-model="book.price"
      />
      <br />
      <label for="salary" class="font-semibold p-1">book_isbn</label>
      <input
        type="number"
        id="isbn"
        name="isbn"
        placeholder=""
        class="border-2 border-black m-1"
        v-model="book.book_isbn"
      />
      <br />
      <button
        class="bg-green-500 p-1 border-2 border-green-500 text-white rounded m-2"
        type="submit"
        @click="submitFormValues"
      >
        Submit
      </button>
      <button
        class="py-1 px-5 bg-black text-white font-bold text-center rounded-md mb-3"
        type="submit"
        @click="getAllEmp"
      >
        GetAll
      </button>
    </form>
    <table class="table-auto border-2 border-black mt-4 place-items-center">
      <thead>
        <tr class="border-2 border-black gap-x-1">
          <th class="border-2 border-black">Book Id</th>
          <th class="border-2 border-black">Book Name</th>
          <th class="border-2 border-black">Author</th>
          <th class="border-2 border-black">Price</th>
          <th class="border-2 border-black">Isbn No</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in state.books"
          :key="item"
          class="border-2 border-black"
        >
          <td class="border-2 border-black text-center">
            {{ item.book_id }}
          </td>
          <td class="text-black border-2 border-black text-center">
            {{ item.book_name }}
          </td>
          <td class="border-2 border-black text-center">
            {{ item.author }}
          </td>
          <td class="border-2 border-black text-center">
            {{ item.price }}
          </td>
          <td class="border-2 border-black text-center">
            {{ item.book_isbn }}
          </td>
          <td>
            <button
              class="mx-3 my-2 p-1 rounded-lg bg-green-600 hover:bg-green-600 text-white w-20"
              type="submit"
              @click="editEmp(book.book_id)"
            >
              Edit
            </button>
            <button
              class="mx-3 my-2 p-1 rounded-lg bg-red-600 hover:bg-red-600 text-white w-20"
              type="submit"
              @click="deletespecificemp"
            >
              Delete
            </button>
          </td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script setup>
let state = reactive({
  books: [],
});
let book = {
  book_id: null,
  book_name: null,
  author: null,
  price: null,
  book_isbn: null,
};
var isEdit = false;
getStudentsAPI();
//================================================= Get API==========================================================
async function getStudentsAPI() {
  console.log("hi");
  state.books = await $fetch("http://localhost:3001/book");
}
//=================================================PUT and POST API====================================================
// async function submitFormValues() {
//   const payload = state.book;
//   const bookId = payload.book_id;
//   delete payload.book_id;
//   if (isEdit === true) {
//     await $fetch("http://localhost:3001/book/" + bookId, {
//       method: "PUT",
//       body: JSON.stringify(payload),
//     });
//     isEdit = false;
//   event.preventDefault();
//   }
//   console.log(book);
//   else {
//   await $fetch("http://localhost:3001/book", {
//     method: "POST",
//     body: book,
//   });
// }
//   getStudentsAPI();
// }
// async function editFormValues(i) {
//   console.log(i);
//   state.book = Object.assign({}, state.books[i]);
//   isEdit = true;
// }

//PUT and POST API
async function submitFormValues() {
  const payload = state.book;
  const bookId = payload.book_id;
  delete payload.book_id;
  if (isEdit === true) {
    await $fetch("http://localhost:3001/book/" + bookId, {
      method: "PUT",
      body: JSON.stringify(payload),
    });
    isEdit = false;
  } else {
    await $fetch("http://localhost:3001/book", {
      method: "POST",
      body: JSON.stringify(payload),
    });
  }
  getStudentsAPI();
}
async function editFormValues(i) {
  console.log(i);
  state.book = Object.assign({}, state.books[i]);
  isEdit = true;
}

//=======================================================DELETE API=============================================
async function deleteFormValues(index) {
  console.log(index);
  await $fetch("http://localhost:3001/book" + index, {
    method: "DELETE",
  });
  getStudentsAPI();
}
</script>
10:47 =========================================================
