<template>
  <div>
    <h1 class="font-extrabold text-center text-5xl mt-8">
      Book Management System
    </h1>
    <div>
      <div>
        <div class="border-black border-4 p-8">
          <form method="post" class="border-black rounded-lg border-4 px-12">
            <h2 class="text-teal-900 text-xl font-bold pt-6">
              Lets Add a Book To Libaray
            </h2>
            <table>
              <label class="pt-10 py-10 mt-4" for="id">Book Id</label>
              <input
                class="border-2 border-black"
                type="text"
                id="book_id"
                name="book_id"
                placeholder=""
                v-model="formData.book_id"
                @change="validationId"
              /><br />
              <span v-for="error in v$.book_id.$errors" :key="error.$uid">{{
                error.$message
              }}</span>
              <br /><br />
              <label for="name">Book Name</label>
              <input
                class="border-2 border-black"
                type="text"
                id="book_name"
                name="book_name"
                placeholder=""
                v-model="formData.book_name"
                @change="validationName"
              /><br />
              <span v-for="error in v$.book_name.$errors" :key="error.$uid">{{
                error.$message
              }}</span>
              <br /><br />
              <label for="author">Book Author</label>
              <input
                class="border-2 border-black"
                type="text"
                id="author"
                name="author"
                placeholder=""
                v-model="formData.author"
                @change="validationAuthor"
              /><br />
              <span v-for="error in v$.author.$errors" :key="error.$uid">{{
                error.$message
              }}</span>
              <br /><br />
              <!-- <label for="image">Book Image</label>
              <input
                class="border-2 border-black"
                type="text"
                id="image"
                name="image"
                placeholder=""
                v-model="formData.book_image"
                @change="validationImage"
              /><br />
              <span v-for="error in v$.book_image.$errors" :key="error.$uid">{{
                error.$message
              }}</span> -->
              <br /><br />
              <label for="price">Book Price</label>
              <input
                class="border-2 border-black"
                type="number"
                id="price"
                name="price"
                placeholder=""
                v-model="formData.price"
                @change="validationPrice"
              /><br />
              <span v-for="error in v$.price.$errors" :key="error.$uid">{{
                error.$message
              }}</span>
              <br /><br />
              <label for="isbn">Book ISbn</label>
              <input
                class="border-2 border-black"
                type="text"
                id="book_isbn"
                name="book_isbn"
                placeholder=""
                v-model="formData.book_isbn"
                @change="validationIsbn"
              /><br />
              <span v-for="error in v$.book_isbn.$errors" :key="error.$uid">{{
                error.$message
              }}</span>
              <br /><br />
              <label for="bookidsearch">Your Book</label>
              <input
                class="border-2 border-black"
                type="text"
                v-model="formData.book_id"
                label="bookidsearch"
              />
              <button
                class="
                  mx-3
                  rounded-lg
                  bg-green-600
                  hover:bg-green-600
                  text-white
                  w-20
                  px-4
                "
                type="button"
                @click="getspecificbook"
              >
                Get Specific Book
              </button>

              <!-- <select name="selectbook" id="selectbook">
                    <option value="category">Book Category</option>
                    <option value="novels">Novels</option>
                    <option value="comics">Comics</option>
                    <option value="scifi">Science Fiction</option>
                    <option value="fantasy">Fantasy</option>
                    <option value="horror">Horror</option>
                    <option value="action">Action</option>
                    <option value="adventure">Adventure</option>
                    <option value="detective">Detective</option>
                    <option value="mystery">Mystery</option>
                    <option value="education">Educational</option>
                    <option value="history">Historical</option>
                    <option value="geographical">Geographical</option>
                    <option value="business">Business</option>
                    <option value="enterpreneurship">Enterpreneurship</option>
                    <option value="fitness">Body Fitness</option>
                    <option value="food">Kitechen Food</option>
                    <option value="spiritual">Spiritual</option>
                </select>     -->
              <div class="mt-10">
                <button
                  class="
                    py-1
                    px-5
                    mr-5
                    bg-black
                    hover:bg-blue-400
                    text-white
                    font-bold
                    text-center
                    rounded-md
                    mb-3
                  "
                  type="submit"
                  @click="formSubmit"
                >
                  Add Book
                </button>
                <button
                  class="
                    py-1
                    px-5
                    bg-black
                    hover:bg-blue-400
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
                <button
                  class="
                    mx-3
                    rounded-lg
                    bg-green-600
                    hover:bg-green-600
                    text-white
                    w-20
                  "
                  @click="getalldata"
                >
                  get all Books
                </button>
              </div>
            </table>
          </form>
          <!-- <div>
            <p>Errors : </p>
            <span v-for="error in v$.errors" :key="error.$uid"></span>
            {{ error.$property }} - {{error.$message}},
        </div> -->
        </div>
        <div class="border-black border-2 m-8 p-8">
          <table class="list">
            <tr>
              <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
              <th class="px-4 border-black rounded-lg border-4">Book Name</th>
              <th class="px-4 border-black rounded-lg border-4">Book Author</th>
              <th class="px-4 border-black rounded-lg border-4">Book Image</th>
              <th class="px-4 border-black rounded-lg border-4">Book Price</th>
              <th class="px-4 border-black rounded-lg border-4">Book ISbn</th>
              <th class="px-4 border-black rounded-lg border-4">Action</th>
            </tr>
            <tr v-for="item in state.items" :key="item">
              <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
              <td class="px-4 border-black rounded-lg border-4">
                {{ item.book_name }}
              </td>
              <td class="px-4 border-black rounded-lg border-4">
                {{ item.author }}
              </td>
              <!-- <td class="px-4 border-black rounded-lg border-4">
                {{ item.book_image }}
              </td> -->
              <td class="px-4 border-black rounded-lg border-4">
                {{ item.price }}
              </td>
              <td class="px-4 border-black rounded-lg border-4">
                {{ item.book_isbn }}
              </td>
              <!-- <td class="px-4 border-green-400 rounded-lg border-4">
                    <img src="{{item.Image}}" alt="" srcset="">
                </td> -->
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
                  @click="deletespecificuser(item.book_id)"
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
                  @click="editBook(item)"
                >
                  Edit
                </button>
              </td>
            </tr>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>


<script setup>
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";
//import { required, minLength, book_id, sameAs, } from "@vuelidate/validators";
const formData = reactive({
  book_id: "",
  book_name: "",
  author: "",
  //   book_image: "",
  price: "",
  book_isbn: "",
  // addedone line extra as array
});
const rules = {
  book_id: { required },
  book_name: { required },
  author: { required },
  //   book_image: { required },
  price: { required },
  book_isbn: { required },
};
const v$ = useVuelidate(rules, formData);
// const submitForm = async () => {
//     const result = await v$.value.$validate();
//     if(result)
//     {
//         alert("successfully done");
//     }
//     else
//     {
//         alert("form is not submitted");
//     }
//     alert("successfully , form is submitted");
// };
import { ref } from "vue";
// how define multiple variable/ref in single reactive state
// Access in html template
// const book_id = ref("");
// const book_name = ref("");
// const book_author = ref("");
// const book_image = ref("");
// const book_price = ref("");
// const book_isbn = ref("");
let state = reactive({
  // allBooks: []
  items: [],
});
getalldata();
async function getalldata() {
  state.items = await $fetch("http://localhost:3001/book");
}
// 2nd part
async function formSubmit() {
  const result = await v$.value.$validate();
  event.preventDefault();
  if (result) {
    // alert("successfully done");
  } else {
    alert("form is not submitted");
  }
  console.log("we are in post", formData.book_id);
  const sampleData = {
    book_id: formData.book_id,
    book_name: formData.book_name,
    author: formData.author,
    // book_image: formData.book_image,
    price: formData.price,
    book_isbn: formData.book_isbn,
  };
  console.log("sample ", sampleData);
  const response = await $fetch("http://localhost:3001/book", {
    method: "POST",
    body: JSON.stringify(sampleData),
  }).then((res) => {
    console.log(alert("successfully done"));
  });
  getalldata();
}
//Delete Api
async function deletespecificuser(book_id) {
  await $fetch("http://localhost:3001/book/" + book_id, {
    method: "DELETE",
  });
  getalldata();
}
//get specific user
async function getspecificbook() {
  console.log(book_id);
  const response = await $fetch("http://localhost:3001/book/" + book_id);
  state.items = [response];
}
getalldata();
async function editBook(book) {
  (formData.book_id = book.book_id),
    (formData.book_name = book.book_name),
    (formData.author = book.author),
    // (formData.book_image = book.book_image),
    (formData.price = book.price),
    (formData.book_isbn = book.book_isbn);
}
async function editBookApi(book) {
  // const response = await fetch("http://localhost:3001/user/" + this.user_id, {
  const response = await $fetch("http://localhost:3001/book/" + book_id.value, {
    method: "PUT",
    headers: {
      "Content-type": "application/json",
    },
    body: JSON.stringify({
      book_id: book_id.value,
      book_name: book_name.value,
      author: author.value,
      //   book_image: book_image.value,
      price: price.value,
      book_isbn: book_isbn.value,
    }),
  });
  console.log(response);
  getalldata();
}
</script>