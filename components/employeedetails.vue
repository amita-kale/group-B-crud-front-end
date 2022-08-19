<template>
  <div class="flex flex-col justify-center items-center block p-4 rounded-lg shadow-lg bg-green-100 max-w-sm">
    <h2 class="flex flex-col justify-center items-center">Employee Details</h2>

    
    <div class="block p-6 rounded-lg shadow-lg bg-white max-w-sm">
        <!-- function name=handleSubmit -->
     <form @submit.prevent="handleSubmit">
      
      <label>Name :</label>
      <input type="text" v-model="Name" name="Name" placeholder="Enter your name"
      class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
      <br/>

      <label>Address :</label>
      <input type="text" v-model="Address" name="Address" placeholder="Enter your Address "
      class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2">
      <br/>

      <label>Contact :</label>
      <input type="text" v-model="Contact" name="Contact" placeholder="Enter your Contact"
      class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
      <br/>


      <label>Salary :</label>
      <input type="text" v-model="Salary" name="Salary" placeholder="Enter amount in Rs."
      class="text-sm text-gray-base w-full  mr-3 py-5 px-4 h-2 border  border-gray-200 rounded mb-2"/>
      <br/>

     
      <label>Department :</label>
      <select class=" dropdown-toggle px-2  py-2 bg-gray-200 text-black font-medium text-xs leading-tight  uppercase rounded shadow-md hover:bg-gray-200 hover:shadow-lg  focus:bg-gray-200 focus:shadow-lg focus:outline-none focus:ring-0
      active:bg-gray-200 active:shadow-lg active:text-black  transition duration-150 ease-in-out flex items-center whitespace-nowrap">
        <option value="Finance">Finance</option>
        <option value="Testing">Testing</option>
        <option value="Software Development">Software Development</option>
        <option value="Management">Management</option>
      </select>
      <br/>
       
     
      

      <div class="terms">
        <input type="checkbox" class="bg-blue-300" required>
        <label>   Accept terms and conditions</label>
      </div>
     
      <br/>
     <button type="submit"   class=" px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md  
         hover:bg-blue-700 hover:shadow-lg  focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0  active:bg-blue-800 active:shadow-lg
         transition duration-150  ease-in-out">  Submit </button>

    </form>
   </div></div>
</template>

<script>


</script>

<style>

</style>