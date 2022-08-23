
<template>
    <div>
        <div>
            <h3 class="p-3 bg-rose-400 font-bold text-center">Project On Crud Application</h3>
            <div class="grid grid-cols-3 text-xl cursor-pointer">
                <NuxtLink to="/students">
                    <div class="mt-20 ml-10 h-20 w-52 bg-emerald-400 font-bold flex items-center justify-center">
                        Students
                    </div>
                </NuxtLink>
                <div class="mt-20 ml-10 h-20 w-52 bg-emerald-400 font-bold flex items-center justify-center">Flights
                </div>
                <div class="mt-20 ml-10 h-20 w-52 bg-emerald-400 font-bold flex items-center justify-center">Users</div>
            </div>
            <div class="grid grid-cols-3 text-xl cursor-pointer ">
                <div class="mt-20 ml-10 h-20 w-52 bg-emerald-400 font-bold flex items-center justify-center">Employees
                </div>
                <div class="mt-20 ml-10 h-20 w-52 bg-emerald-400 font-bold flex items-center justify-center">Books</div>
                 <NuxtLink to="/product">
                    <div class="mt-20 ml-10 h-20 w-52 bg-emerald-400 font-bold flex items-center justify-center">Products</div>
                 </NuxtLink>
                
            </div>
        </div>

    </div>

</template>
<script setup lang="ts">
</script>