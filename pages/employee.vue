

<template>
<!-- <div class="flex flex-col justify-center items-center width=300px">
  <input type="text" name="search" placeholder="search here!" v-model="data.search" class=" text-sm text-black">
  <button>Products</button>
</div> -->

  <div class=" flex flex-col justify-center items-center width=250px">

    <h2 class="flex flex-col justify-center items-center">Employee Details</h2>
      <form name="empform" method="POST" >
        <label for="EmployeeName">Name :</label>
        <input  type="text"  name="EmployeeName" id="EmployeeName" placeholder="Enter your name" v-model="data.EmployeeName" class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
        <!-- :v="v$.EmployeeName" -->
        <br/>
        
        <label for="EmployeeAddress">Address :</label>
        <input  type="text"  name="EmployeeAddress" placeholder="Enter your Address " id="EmployeeAddress" v-model="data.EmployeeAddress"
        class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2">
        <!-- :v="v$.EmployeeAddress" -->
        <br/>

        <label for="contact" >Contact :</label>
        <input  type="text"  id="contact" name="contact" placeholder="Enter your Contact" v-model="data.contact"
        class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
        <!-- :v="v$.contact"  -->
              
        <br/>
        <label for="salary" >Salary :</label>
        <input  type="text" id="salary" name="salary" placeholder="Enter amount in Rs." v-model="data.salary"
         class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
        <!--  :v="v$.salary" -->
              
        
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

<!-- <script lang="ts">
import useVuelidate,{
  required, EmployeeName, EmployeeAddress, contact, salary,
}from '~/utils/vuelidate/useVuelidate';
export default{
  name:'empform',
}
</script> -->

<script setup lang="ts">
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
  employee: [],  ///allemp state=empp sampledata=data
  
});
// GETAPI
getEmployeeApi();
async function getEmployeeApi(){
  console.log("get a api call");
  state.employee = await $fetch("http://localhost:3001/emp/details");

}//working

// POSTAPI
async function SubmitForm() {
  if(Edit==false){
  await $fetch("http://localhost:3001/emp/details/",{
    method: 'POST',
    body: (data),
  }); 
   getEmployeeApi();

  }
  if(Edit==true){
     console.log(employeedetails);
  const response = await $fetch("http://localhost:3001/emp/details/" + tempId,{
      method: "PATCH",
      body: (data),
    }
  );
  Edit=false;
   getEmployeeApi();
  }
  getEmployeeApi();
}//working


//Patch api
// yet to work
async function EditForm(id) {
  Edit=true;
  tempId = id;
 employeedetails = state.employee.filter((emp) => {
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



//deleteapi
async function DeleteForm(id) {
 await $fetch("http://localhost:3001/emp/details/"+ id, {
  method:'DELETE',
  });
  Edit=false;
  getEmployeeApi();  
}//working  


// const validate = {
//   EmployeeName: {require , EmployeeName},
//   EmployeeAddress :{require, EmployeeAddress},
//   contact:{required, contact},
//   salary:{required, salary},
// };
// const v$ = useVuelidate(validate, state.employee);


// async function EditForm(id: string) 
// {
//       let editspecificfeild = await $fetch("http://localhost:3001/emp/details/" +id );
//       console.log("updation :",editspecificfeild);
//       //alert(editspecificfeild.id);
//      // data.id = editspecificfeild.id;
//       data.EmployeeName = editspecificfeild.EmployeeName;
//       data.EmployeeAddress = editspecificfeild.EmployeeAddress;
//       data.contact = editspecificfeild.contact;
//       data.salary = editspecificfeild.salary;
     
//       const tobeeditdata = {
//       // id: data.id,
//         EmployeeName : data.EmployeeName,
//         EmployeeAddress : data.EmployeeAddress,
//         contact : data.contact,
//         salary: data.salary,
       

//       };
//       if(Edit == true){
//         const response = await $fetch("http://localhost:3001/emp/update/"+ id,{
//           method : 'PATCH',
//           body : JSON.stringify(tobeeditdata),
//        })
//       }
    
//          // Edit= false;
//           getEmployeeApi();
           
// }


</script>






 


