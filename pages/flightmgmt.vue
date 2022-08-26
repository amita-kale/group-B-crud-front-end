<template>
  <div class=" flex flex-col justify-center items-center width=250px">
    <div>
      <div>Ticket
        <input type="number" v-model="data.flightData.ticket"
          class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"
          placeholder="Ticket Number" /><span v-for="error in v$.ticket.$errors" :key="error.$uid"
          class="text-red-500">{{ error.$message }}</span>

      </div>
      <div>
        Passenger<input type="text" v-model="data.flightData.passenger"
          class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"
          placeholder="Passenger Name" /><span v-for="error in v$.passenger.$errors" :key="error.$uid"
          class="text-red-500">{{ error.$message }}</span></div>
      <div>Destination
        <input type="text" v-model="data.flightData.Destination"
          class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"
          placeholder="Destination" /><span v-for="error in v$.Destination.$errors" :key="error.$uid"
          class="text-red-500">{{ error.$message }}</span>
      </div>
      <div><button @click="alldata">Get All</button></div>
      <div><button @click="postall">Add</button></div>
      <div>
        <input type=" number" v-model="data.flightData.ticket" />
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
            <button @click="editUser(item.ticket)" class="">Edit</button>
          </td>
          <td class="border-2">
            <button @click="deletespecificuser(item.ticket)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script lang="ts" >import useVuelidate, {
  required, minLength, maxLength
} from '../utlis/vuelidate/useVuelidate';
</script>
<script setup lang="ts">
// import useVuelidate from "@vuelidate/core";
import { reactive, ref } from "vue";

let data = reactive({
  flightData: {
    ticket: "",
    passenger: "",
    Destination: ""
  }
});
const rules = {
  ticket: {
    required, minLength: minLength(2),
    maxLength: maxLength(3),
  },
  passenger: {
    required, minLength: minLength(3),
    maxLength: maxLength(5)
  },
  Destination: {
    required, minLength: minLength(3),
    maxLength: maxLength(5)
  },
}

let state = reactive({
  select: true,//boolean type 
  items: [],
  id: '',
});
const v$ = useVuelidate(rules, data.flightData)
alldata();
async function alldata() {
  state.items = await $fetch("http://localhost:3001/flight-m");
}
async function post() {
  const sampleData = {
    ticket: data.flightData.ticket,
    passenger: data.flightData.passenger,
    Destination: data.flightData.Destination,
  };

  console.log("we are in post");
  const result = await v$.value.$validate();
  if (result) {
    // if (response == 200) {
    const response = await $fetch("http://localhost:3001/flight-m", {
      method: "POST",
      body: JSON.stringify(sampleData),
    });
    alldata();
    // } else {
    //   alert("Error is catched from backend")

    // }
  } else {
    alert("ache se value daal  ghada")
  }
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
    "http://localhost:3001/flight-m/" + data.flightData.ticket
  );
}
async function editUser(id) {
  state.select = false;
  const edit: any = await $fetch("http://localhost:3001/flight-m/" + id);
  data.flightData.ticket = edit.ticket;
  data.flightData.passenger = edit.passenger;
  data.flightData.Destination = edit.Destination;
  state.id = edit.ticket;


}
async function put(id) {
  const sampleData = {
    ticket: data.flightData.ticket,
    passenger: data.flightData.passenger,
    Destination: data.flightData.Destination,
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
