

<template>
  
    <h2 class="flex flex-col justify-center items-center">Employee Details</h2>

    
    
       
     <form method="POST">
      <table>
        <tr>
             <td>  <label >Name :</label></td>
              <td>  <input type="text" v-model="state.employee.EmployeeName" name="Name" placeholder="Enter your name"
                class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/></td>
                <br/>
                </tr>

          <tr>  <td>  <label >Address :</label></td>
              <td> <input type="text" v-model="state.employee.EmployeeAddress" name="Address" placeholder="Enter your Address "
                class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"></td> 
                <br/>
          </tr>
           <tr>
              <td> <label >Contact :</label></td>
              <td>  <input type="text" v-model="state.employee.contact" name="Contact" placeholder="Enter your Contact"
                class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/></td>
                <br/>
          </tr>
          <tr>

              <td>  <label >Salary :</label></td>
               <td><input type="text" v-model="state.employee.salary" name="Salary" placeholder="Enter amount in Rs."
                class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/></td>
                <br/>
          </tr>
          <tr>
              
              <td>  <label >Department :</label></td>
               <td> <select class=" dropdown-toggle px-2  py-2 bg-gray-200 text-black font-medium text-xs leading-tight  uppercase rounded shadow-md hover:bg-gray-200 hover:shadow-lg  focus:bg-gray-200 focus:shadow-lg focus:outline-none focus:ring-0
                active:bg-gray-200 active:shadow-lg active:text-black  transition duration-150 ease-in-out flex items-center whitespace-nowrap" v-model="department">
                  <option value="Finance">Finance</option>
                  <option value="Testing">Testing</option>
                  <option value="Software Development">Software Development</option>
                  <option value="Management">Management</option>
                </select></td> <br/>
                
                   <div class="terms">
        <input type="checkbox" class="bg-blue-300" required>
        <label>   Accept terms and conditions</label>
      </div>
    

                </tr>
                </table>
               
       
     
      

   
      <br/>
     <button type="submit"   class=" px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md  
         hover:bg-blue-700 hover:shadow-lg  focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0  active:bg-blue-800 active:shadow-lg
         transition duration-150  ease-in-out" v-on:click="SubmitForm()">  Submit </button>

         <!-- <button type="edit"   class=" px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md  
         hover:bg-blue-700 hover:shadow-lg  focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0  active:bg-blue-800 active:shadow-lg
         transition duration-150  ease-in-out" @click="Editform">  Edit </button> -->

    </form>
    <table>
      <tr>
        <td><th>EmployeeId</th></td>
        <td><th> EmployeeName</th></td>
        <td><th>EmployeeAddress </th></td>
        <td><th>Contact </th></td>
        <td><th> Salary</th></td>
        <td><th>Department</th></td>
        <td><th colspan="2">To do</th></td>
       
      </tr>

      <tr v-for="(employee,id) in state.employee" :key="employee" >
        <td>{{employee.EmployeeId}}</td>
        <td>{{employee.EmployeeName}}</td>
        <td>{{employee.EmployeeAddress}}</td>
        <td>{{employee.contact}}</td>
        <td>{{employee.salary}}</td>
        <td>{{employee.department}}</td>
        <td>
          <button class="border-solid bg-blue-200 " v-on:click="EditForm(id)">Edit</button>
        </td>
        <td>
          <button class="border-solid bg-blue-200" v-on:click="DeleteForm(employee.id)">Delete</button>
        </td>
        
      </tr>
    </table>
  
</template>

<script setup lang="ts">

var FormEdit: boolean = false;

let state = reactive({
  Employees: [],
  employee:{
    //EmployeeId: ,
    EmployeeName: null,
    EmployeeAddress: null,
    contact:null,
    salary:null,
    department:null
  }
});
getEmployeeApi();

async function getEmployeeApi(){
  console.log("get a api call");
  state.Employees = await $fetch("localhost:3001/emp");

}

//put and post
async function SubmitForm() {
  const payload = state.employee;
  const id = payload.id;
  delete payload.id;
  if(FormEdit === true){
    await $fetch("localhost:3001/emp"+id,{  //api
      method: 'PUT',
      body: JSON.stringify(payload)
  });
  FormEdit =false;
  
} 
else{
  await $fetch("localhost:3001/emp",{
    method:'POST',
    body: JSON.stringify(payload)
  });
}
 //
 getEmployeeApi();
 state.employee = {
  //EmployeeId: '',
  EmployeeName:'',
  EmployeeAddress:'',
  contact:'',
  salary:'',
  department:'',
 }
}
async function EditForm(id) {
  console.log(id);
  state.employee = Object.assign({},state.Employees[id]);
  FormEdit = true;
  
}

//deleteapi
async function DeleteForm(id) {
  console.log(id);
  await $fetch("localhost:3001/emp"+id, {
method:'DELETE'
  });
  getEmployeeApi();

  
}
</script>

<style>

</style>