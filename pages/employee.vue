



<template>

  <div class=" flex flex-col justify-center items-center width=250px">

    <h2 class="flex flex-col justify-center items-center">Employee Details</h2>
      <form name="empform" method="POST" >
        <label for="EmployeeName">Name :</label>
        <input  type="text"  name="EmployeeName" id="EmployeeName" placeholder="Enter your name" v-model="data.EmployeeName" class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
        <!-- :v="v$.EmployeeName" -->
        <span v-for="error in v$.EmployeeName.$errors" :key="error.$uid" class="text-blue-500" >{{ error.$message }}</span>
        <br/>
        
        <label for="EmployeeAddress">Address :</label>
        <input  type="text"  name="EmployeeAddress" placeholder="Enter your Address " id="EmployeeAddress" v-model="data.EmployeeAddress"
        class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2">
        <!-- :v="v$.EmployeeAddress" -->
        <span v-for="error in v$.EmployeeAddress.$errors" :key="error.$uid" class="text-blue-500">{{ error.$message }}</span>
        <br/>

        <label for="contact" >Contact :</label>
        <input  type="text"  id="contact" name="contact" placeholder="Enter your Contact" v-model="data.contact"
        class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
        <!-- :v="v$.contact"  -->
        <span v-for="error in v$.contact.$errors" :key="error.$uid" class="text-blue-500" >{{ error.$message }}</span>
              
        <br/>
        <label for="salary" >Salary :</label>
        <input  type="text" id="salary" name="salary" placeholder="Enter amount in Rs." v-model="data.salary"
         class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
        <!--  :v="v$.salary" -->
        <span v-for="error in v$.salary.$errors" :key="error.$uid" class="text-blue-500">{{ error.$message }}</span>
              
        
        <br/>
      
        <button type="button"   class=" px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md  
          hover:bg-blue-700 hover:shadow-lg  focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0  active:bg-blue-800 active:shadow-lg
          transition duration-150  ease-in-out" id="SubmitForm" @click="SubmitForm()">  Submit </button>
      </form>
  </div >
  <br/>  
  <div class="flex flex-col justify-center items-center width=250px">
    <table class="border border-solid">
      <tr>
        <td><th> EmployeeName</th></td>
        <td><th>EmployeeAddress </th></td>
        <td><th>Contact </th></td>
        <td><th> Salary</th></td>
        <td><th colspan="2">Operations</th></td>
      </tr>

      <tr v-for="(employee) in state.employee" :key="employee.id" >
        <td>{{employee.EmployeeName}}</td>
        <td>{{employee.EmployeeAddress}}</td>
        <td>{{employee.contact}}</td>
        <td>{{employee.salary}}</td>
        <td>
          <button class="border-solid bg-blue-200 " id="EditForm" @click="EditForm(employee.id)">Edit</button>
        </td>
        <td>
          <button class="border-solid bg-blue-200" id="DeleteForm" @click="DeleteForm(employee.id)">Delete</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script lang="ts">
import useVuelidate,{ required, minLength, maxLength}from '~/utils/vuelidate/useVuelidate';
export default {
  name:'empform',
}
</script> 

<script setup lang="ts">

// import useVuelidate from "@vuelidate/core";
// import { maxLength, minLength, required } from "@vuelidate/validators";


let employeedetails;
let tempId;
var Edit= false;
let data= reactive ( { 
    EmployeeName : '',
    EmployeeAddress : '',
    contact: '',
    salary: ''
  });

let state = reactive({
  employee: [],  
  
});
// GETAPI
getEmployeeApi();
async function getEmployeeApi(){
  console.log("get a api call");
  state.employee = await $fetch("http://localhost:3001/emp/details");

}//working

// POSTAPI /PATCHAPI
async function SubmitForm() {
  if(Edit==false){
    const result = await v$.value.$validate();
    if(result){
      console.log("validate");
    }
  await $fetch("http://localhost:3001/emp/details/",{
    method: 'POST',
    body: (data),
  }); 
   getEmployeeApi();

  }
  if(Edit==true){
     console.log(employeedetails);
     await $fetch("http://localhost:3001/emp/details/" + tempId,{
      method: "PATCH",
      body: (data),
    }
  );
  Edit=false;
   getEmployeeApi();
  }
  getEmployeeApi();
}//working


//PATCH API
async function EditForm(id) {
  Edit=true;
  tempId = id;
  employeedetails = state.employee.filter((emp:any) => {
    if (id == emp.id) {
      data.EmployeeName = emp.EmployeeName;
      data.EmployeeAddress = emp.EmployeeAddress;
      data.contact = emp.contact;
      data.salary = emp.salary;
      return emp;
    }
  });
    getEmployeeApi(); 
}
//DELETE API
async function DeleteForm(id) {
 await $fetch("http://localhost:3001/emp/details/"+ id, {
  method:'DELETE',
  });
  Edit=false;
  getEmployeeApi();  
}//working  

let details= {
  emp:{ 
    EmployeeName : '',
    EmployeeAddress : '',
    contact: '',
    salary: ''
  }};

const rules = {
  EmployeeName: {
    required,
    minLength: minLength(2),
    maxLength: maxLength(3),
  },
  EmployeeAddress: {
    required, 
    minLength: minLength(3),
    maxLength: maxLength(5)
  },
  contact: {
    required,
    minLength: minLength(3),
    maxLength: maxLength(5)
  },
  salary: {
    required,
    minLength: minLength(3),
    maxLength: maxLength(5)
  }
}
const v$ = useVuelidate(rules, details.emp);

</script>




 


