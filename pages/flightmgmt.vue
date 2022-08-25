<template>
  <div class=" flex flex-col justify-center items-center width=250px">
    <div>
      <div><input type="number" v-model="ticket"
          class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"
          placeholder="Ticket Number" required />Ticket</div>
      <div><input type="text" v-model="passenger"
          class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"
          placeholder="Passenger Name" required />Passenger</div>
      <div><input type="text" v-model="Destination"
          class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"
          placeholder="Destination" required />Destination</div>
      <div><button @click="alldata">Get All</button></div>
      <div><button @click="postall()">Add</button></div>
      <div>
        <input type=" number" v-model="ticket" />
        <button type="button" @click="getspecifictickets">
          Get Specific Ticket
        </button>
      </div>
    </div>
    <table :item="items" id="showdata" class="flex flex-col justify-center items-center width=250px">
      <tbody>
        <th class="border-2">Ticket</th>
        <th class="border-2">Passenger</th>
        <th class="border-2">Destination</th>

        <th class="border-2" colspan="2">Action</th>
        <tr v-for="item in state.items" :key="item">
          <td class="border-2">{{ item.ticket }}</td>
          <td class="border-2">{{ item.passenger }}</td>
          <td class="border-2">{{ item.Destination }}</td>

          <td class="border-2">
            <button @click="editUser(item.ticket)">Edit</button>
          </td>
          <td class="border-2">
            <button @click="deletespecificuser(item.ticket)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script setup lang="ts">
import { reactive, ref } from "vue";

let ticket = ref("");//this should also uncommit
let passenger = ref("");
let Destination = ref("");

let state = reactive({
  select: true,//boolean type 
  items: [],
  id: '',
});

let flightData = reactive({ //reactive and ref is use for  composition api
  ticket: '',
  passenger: '',
  Destination: '',
});

//Validation

alldata();

async function alldata() {
  state.items = await $fetch("http://localhost:3001/flight-m");
}

async function post() {
  console.log("we are in post", ticket.value);
  const sampleData = {
    ticket: ticket.value,
    passenger: passenger.value,
    Destination: Destination.value,
  };
  const response = await $fetch("http://localhost:3001/flight-m", {
    method: "POST",
    body: JSON.stringify(sampleData),
  });
  alldata();
}
function postall() {
  if (state.select === true) {
    post();

  } else {
    const id = state.id;
    put(id);
  }
}
async function deletespecificuser(ticket) {
  await $fetch("http://localhost:3001/flight-m/" + ticket, {
    method: "DELETE",
  });
  alldata();
}

async function getspecifictickets() {
  const response = await $fetch(
    "http://localhost:3001/flight-m/" + ticket.value
  );
}
async function editUser(id) {
  state.select = false;
  const edit: any = await $fetch("http://localhost:3001/flight-m/" + id);
  ticket.value = edit.ticket;
  passenger.value = edit.passenger;
  Destination.value = edit.Destination;
  state.id = edit.ticket;


}
async function put(id) {
  const sampleData = {
    ticket: ticket.value,
    passenger: passenger.value,
    Destination: Destination.value,
  };

  console.log(id, sampleData);

  await $fetch("http://localhost:3001/flight-m/" + id, {
    method: "PUT",
    body: JSON.stringify(sampleData),
  });

  alldata();
  state.select = true;
}

</script>
