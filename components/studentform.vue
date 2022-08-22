 <template>
    <div>
        <div class="grid gap-x-7  grid-cols-3 h-screen">
            <div
                class="border-solid border-2 border-amber-600 drop-shadow-md bg-gradient-to-r from-indigo-200 via-purple-200 to-pink-200 ">
                <form>
                    <h1 style="color: red" class="font-bold text-3xl p-6">Add Students</h1>
                    <table>

                        <tr>
                            <td><label>Full Name:</label></td>
                            <td><input type="text"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="student.full_name"></td>
                        </tr>
                        <tr>
                            <td><label>Email :</label></td>
                            <td><input type="email"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="student.email"></td>
                        </tr>
                        <tr>
                            <td><label>Contact</label></td>
                            <td><input type="number"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="student.contact"></td>
                        </tr>
                        <tr>
                            <td><label>Address</label></td>
                            <td><textarea class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="student.address"></textarea>
                            </td>
                        </tr>
                        <tr>
                            <td><label>Student Profile:</label></td>
                            <td><input type="file"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-2 pr-2 ml-2 mb-2 w-52">
                            </td>
                        </tr>
                    </table>
                    <button type="button" v-on:click="submitFormValues()" class="border-solid rounded border-2 border-indigo-600 p-3 ml-36 mt-3
                 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500">Submit</button>
                </form>
            </div>
            <div class="bg-gray-300 col-span-2">

                <input
                    class="placeholder:italic placeholder:text-slate-400 block bg-white w-50 border border-slate-300 rounded-md m-10 py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm"
                    placeholder="Search for anything..." type="text" name="search" />
                <table class=" border-black-400 border-separate bg-white  border border-slate-400 m-20">
                    <tr>
                        <th class="border border-slate-300">StudentID</th>
                        <th class="border border-slate-300">FullName</th>
                        <th class="border border-slate-300">Email</th>
                        <th class="border border-slate-300">Contact</th>
                        <th class="border border-slate-300">Address</th>
                        <th class="border border-slate-300">StudentProfile</th>
                        <th colspan="2" class="border border-slate-300">Action</th>

                    </tr>
                    <tr v-for="(stud) in students" :key="stud">

                        <td class="border border-slate-300">{{ stud.student_id }}</td>
                        <td class="border border-slate-300">{{ stud.full_name }}</td>
                        <td class="border border-slate-300">{{ stud.email }}</td>
                        <td class="border border-slate-300">{{ stud.contact }}</td>
                        <td class="border border-slate-300">{{ stud.address }}</td>
                        <td class="border border-slate-300"><a>{{ stud.student_profile }}</a></td>
                        <td class="border border-slate-300">
                            <button class="
                border-solid
                rounded
                border-2 border-indigo-600
                p-1
                bg-gradient-to-r
                from-indigo-500
                via-purple-500
                to-pink-500
              ">
                                Edit
                            </button>
                        </td>
                        <td class="border border-slate-300">
                            <button class="
                border-solid
                rounded
                border-2 border-indigo-600
                p-1
                bg-gradient-to-r
                from-indigo-500
                via-purple-500
                to-pink-500
              ">
                                Delete
                            </button>
                        </td>
                    </tr>

                </table>

            </div>
        </div>

    </div>
</template>

<script setup lang="ts">


let students: any = [];
// const students: Array<object> = [];
const student = {
    student_id: null,
    full_name: null,
    email: null,
    contact: null,
    address: null,
    student_profile: null
}

const { data: count } = useFetch("http://localhost:3002/student");
students = count;
// let bookDetail = count;
console.log(count[0]);



function submitFormValues() {
    this.students.push(this.student);
    // students.push(count[0]);

}

</script>



