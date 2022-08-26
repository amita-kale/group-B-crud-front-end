

<script setup>
import { ref } from "vue";
// how define multiple variable/ref in single reactive state
// Access in html template
const user_id = ref("");
const email = ref("");
const name = ref("");
const gender = ref("");
const mobile_number = ref("");
const address = ref("");
let state = reactive({
    // allBooks: []
    items: [],
});
//------------------------------------------------------Ist------------------
getalldata();
// GET API
async function getalldata() {
    state.items = await $fetch("http://localhost:3001/user");
}
async function save() {
    console.log("we are in post", user_id.value);
    const sampleData = {
        user_id: user_id.value,
        email: email.value,
        name: name.value,
        gender: gender.value,
        mobile_number: mobile_number.value,
        address: address.value,
    };
    const response = await $fetch("http://localhost:3001/user", {
        method: "POST",
        body: JSON.stringify(sampleData),
    });
    getalldata();
}
//getspecific user
async function getspecificuser() {
    console.log(user_id);
    const response = await $fetch("http://localhost:3001/user/" + user_id.value);
    state.items = [response];
}
//Delete Api
async function deletespecificuser(user_id) {
    await $fetch("http://localhost:3001/user/" + user_id, {
        method: "DELETE",
    });
    getalldata();
}
async function editUser(user) {
    (this.user_id = user.user_id),
        (this.name = user.name),
        (this.mobile_number = user.mobile_number),
        (this.gender = user.gender),
        (this.email = user.email),
        (this.address = user.address);
}
async function editUserApi(user) {
    // const response = await fetch("http://localhost:3001/user/" + this.user_id, {
    const response = await $fetch("http://localhost:3001/user/" + user_id.value, {
        method: "PUT",
        headers: {
            "Content-type": "application/json",
        },
        body: JSON.stringify({
            user_id: user_id.value,
            email: email.value,
            name: name.value,
            gender: gender.value,
            mobile_number: mobile_number.value,
            address: address.value,
        }),
    });
    console.log(response);
    getalldata();
}
</script>
<style scoped>
body {
    justify-content: space-around;
    align-items: center;
    height: 60vh;
    display: grid;
    flex-direction: column;
    font-family: sans-serif;
}

.form {
    position: relative;
    width: 20%;
    height: 60px;
    overflow: hidden;
}

.form input {
    width: 100%;
    height: 100%;
    color: #595F6E;
    padding-top: 20px;
    border: none;
    outline: none;
}

.form label {
    position: absolute;
    bottom: 0px;
    left: 0%;
    width: 100%;
    height: 100%;
    pointer-events: none;
    border-bottom: 1px solid black;
    /* transition: top 200ms ease-in, left 200ms ease-in, font-size 200ms ease-in; */
}

.form label::after {
    position: absolute;
    content: "";
    bottom: -1px;
    left: 0px;
    width: 100%;
    height: 100%;
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    border-bottom: 3px solid #5FA8D3;
    /* transition: top 200ms ease-in, left 200ms ease-in, font-size 200ms ease-in; */
}

.content-name {
    position: absolute;
    bottom: 5px;
    transition: all 0.3s ease;
    left: 0px;
    transition: all 0.3s ease;
}

.form input:focus+.label-name .content-name,
.form input:valid+.label-name .content-name {
    transform: translateY(-150%);
    font-size: 14px;
    color: #5FA8D3;
}

.form input:focus+.label-name::after,
.form input:valid+.label-name::after {
    transform: translateX(0%);
}
</style>
<template>
    <div class="">
        <!-- <link
      href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css"
      rel="stylesheet"
    /> -->
        <form method="POST" class="justify-center">
            <div class="form bg-black">
                <input type="text" v-model="user_id" name="name" autocomplete="off" required
                    class="focus:border-blue-500" />
                <label for="user_id" class="label-name">
                    <span class="content-name">User Id</span>
                </label>
            </div>
            <div class="form bg-black">
                <input type="text" v-model="name" name="name" autocomplete="on" required
                    class="focus:border-blue-500" />
                <label for="name" class="label-name">
                    <span class="content-name">Name</span>
                </label>
            </div>
            <div class="form bg-black">
                <input type="text" v-model="gender" name="name" autocomplete="off" required
                    class="focus:border-blue-500" />
                <label for="gender" class="label-name">
                    <span class="content-name">Gender</span>
                </label>
            </div>
            <div class="form bg-black">
                <input type="text" v-model="address" name="name" autocomplete="off" required
                    class="focus:border-blue-500" />
                <label for="address" class="label-name">
                    <span class="content-name">Address</span>
                </label>
            </div>
            <div class="form bg-black">
                <input type="text" v-model="email" name="name" autocomplete="off" required
                    class="focus:border-blue-500" />
                <label for="email" class="label-name">
                    <span class="content-name">Email</span>
                </label>
            </div>
            <div class="form bg-black">
                <input type="number" v-model="mobile_number" name="name" autocomplete="off" required
                    class="focus:border-blue-500" />
                <label for="mobile_number" class="label-name">
                    <span class="content-name">Mobile</span>
                </label>
            </div>
            <button type="button" @click="editUserApi">Update</button>
            <button type="button" @click="save" onclick="save()">>Add</button>
            <button type="button" @click="getalldata" onclick="getalldata()">
                Get All DAta
            </button>
            <label for="id">Your Id</label>
            <input type="text" v-model="user_id" label="id" />
            <button type="button" @click="getspecificuser" onclick="getspecificuser()">
                Get Specific User
            </button>
        </form>
        <!--
    <div v-once v-show="show">
      {{ getalldata() }}
    </div> -->
        <table :item="items" id="showdata">
            <tbody>
                <th class="border-2">User ID</th>
                <th class="border-2">Name</th>
                <th class="border-2">EMAIL</th>
                <th class="border-2">ADDRESS</th>
                <th class="border-2">GENDER</th>
                <th class="border-2">MOBILE NUMBER</th>
                <th class="border-2" colspan="2">Action</th>
                <tr v-for="item in state.items" :key="item">
                    <td class="border-2">{{ item.user_id }}</td>
                    <td class="border-2">{{ item.name }}</td>
                    <td class="border-2">{{ item.email }}</td>
                    <td class="border-2">{{ item.address }}</td>
                    <td class="border-2">{{ item.gender }}</td>
                    <td class="border-2">{{ item.mobile_number }}</td>
                    <td class="border-2">
                        <button @click="editUser(item)">Edit</button>
                    </td>
                    <td class="border-2">
                        <button @click="deletespecificuser(item.user_id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
        <br />
    </div>
</template>















