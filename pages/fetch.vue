<script setup>
const { data: count } = await useFetch("http://localhost:3001/book");
let userData = count;
console.log("product name =", typeof count);
console.log("product name =", count);
// dataFetch = () => {
//     const { data: count } = await useFetch('http://localhost:8080/feed/allData')
//     data = () => {
//         return count
//     }
// }
// ///////////////////////////////////////
// const { data, pending, error, refresh } = await useFetch(
//     'http://localhost:8080/feed/allData',
//     {
//         pick: ['productName']
//     }
// )
// console.log(data.productName)
</script>
<template>
  <div class="border-black border-2 m-8 p-8">
    <table class="list">
      <tr>
        <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
        <th class="px-4 border-green-400 rounded-lg border-4">book_id</th>
        <th class="px-4 border-green-400 rounded-lg border-4">book_name</th>
        <th class="px-4 border-green-400 rounded-lg border-4">author</th>
        <th class="px-4 border-green-400 rounded-lg border-4">price</th>
        <th class="px-4 border-green-400 rounded-lg border-4">book_image</th>
        <th class="px-4 border-green-400 rounded-lg border-4">book_isbn</th>

        <th class="px-4 border-green-400 rounded-lg border-4">Action</th>
      </tr>
      <tr v-for="(item, index) in userData" v-bind:index="index" :key="item">
        <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
        <td class="px-4 border-green-400 rounded-lg border-4">
          {{ item.book_id }}
        </td>
        <td class="px-4 border-green-400 rounded-lg border-4">
          {{ item.book_name }}
        </td>
        <td class="px-4 border-green-400 rounded-lg border-4">
          {{ item.author }}
        </td>
        <td class="px-4 border-green-400 rounded-lg border-4">
          {{ item.price }}
        </td>
        <td class="px-4 border-green-400 rounded-lg border-4">
          <img src="{{item.book_image}}" alt="" srcset="" />
        </td>
        <td class="px-4 border-green-400 rounded-lg border-4">
          {{ item.book_isbn }}
        </td>
        <td class="px-4 border-green-400 rounded-lg border-4">
          {{ item.Action }}
          <button
            class="mx-3 rounded-lg bg-red-600 hover:bg-red-700 text-white w-20"
            @click="userDelete(index)"
          >
            Delete
          </button>
          <button
            class="mx-3 rounded-lg bg-green-600 hover:bg-green-600 text-white w-20"
            @click="onEdit(index)"
          >
            Edit
          </button>
        </td>
      </tr>
    </table>
  </div>
</template>
