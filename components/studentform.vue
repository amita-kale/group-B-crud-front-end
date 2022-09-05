 <template>
    <div>


        <div class="grid gap-x-7  grid-cols-3 h-screen">
            <div
                class="border-solid border-2 border-amber-600 drop-shadow-md bg-gradient-to-r from-indigo-200 via-purple-200 to-pink-200 ">
                <form class="space-y-6">
                    <h1 style="color: red" class="font-bold text-3xl p-6">Add Students</h1>
                    <table>

                        <tr>
                            <td><label>Full Name:</label></td>
                            <td><input type="text"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="state.student.full_name" :v="v$.full_name">
                            </td>
                        </tr>
                        <tr>
                            <td></td>
                            <td><span v-for="error in v$.full_name.$errors" :key="error.$uid"
                                    class="text-red-600 text-xs pl-4">{{ error.$message }}</span>
                            </td>
                        </tr>
                        <tr>
                            <td><label>Email :</label></td>
                            <td><input type="email"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="state.student.email"></td>
                        </tr>
                        <tr>
                            <td></td>
                            <td><span v-for="error in v$.email.$errors" :key="error.$uid"
                                    class="text-red-600 text-xs pl-4">{{ error.$message }}</span>
                            </td>
                        </tr>
                        <tr>
                            <td><label>Contact</label></td>
                            <td><input type="number"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="state.student.contact"></td>
                        </tr>
                        <tr>
                            <td></td>
                            <td><span v-for="error in v$.contact.$errors" :key="error.$uid"
                                    class="text-red-600 text-xs pl-4">{{ error.$message }}</span>
                            </td>
                        </tr>


                        <tr>
                            <td><label>Address</label></td>
                            <td><textarea class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="state.student.address"></textarea>
                            </td>
                        </tr>
                        <tr>
                            <td></td>
                            <td><span v-for="error in v$.address.$errors" :key="error.$uid"
                                    class="text-red-600 text-xs pl-4">{{ error.$message }}</span>
                            </td>
                        </tr>
                        <tr>
                            <td><label>Subject</label></td>
                            <td>
                                <select class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"
                                    v-model="state.subject_id" multiple="true">
                                    <option v-for="sub in state.subjects" :key="sub.subject_id" :value="sub.subject_id">
                                        {{ sub.subject_id }} {{ sub.sub_name }}
                                    </option>

                                </select>
                                {{ state.subject_id }}
                            </td>
                        </tr>
                        <!-- <tr>
                            <td>{{ state.subject1 }}</td>
                            <td><span v-for="error in v$.subject.$errors" :key="error.$uid"
                                    class="text-red-600 text-xs pl-4">{{ error.$message }}</span>
                            </td>
                        </tr> -->
                        <!-- <tr>
                            <td><label>Student Profile:</label></td>
                            <td><input type="file"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-2 pr-2 ml-2 mb-2 w-52">
                            </td>
                        </tr> -->
                    </table>
                    <button type="button" v-on:click="submitFormValues()" class="border-solid rounded border-2 border-indigo-600 p-3 ml-36 mt-3
                 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500">Submit</button>
                </form>
            </div>
            <div class="bg-gray-300 col-span-2">

                <input
                    class="placeholder:italic placeholder:text-slate-400 block bg-white w-50 border border-slate-300 rounded-md m-10 py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm"
                    placeholder="Search for anything..." type="text" @input="searchInput($event)" name="search" />
                <table class=" border-black-400 border-separate bg-white  border border-slate-400 m-20">
                    <tr>
                        <th class="border border-slate-300">StudentID</th>
                        <th class="border border-slate-300">FullName</th>
                        <th class="border border-slate-300">Email</th>
                        <th class="border border-slate-300">Contact</th>
                        <!-- <th class="border border-slate-300">Gender</th> -->
                        <th class="border border-slate-300">Address</th>
                        <!-- <th class="border border-slate-300">SubjectID</th> -->
                        <!-- <th class="border border-slate-300">StudentProfile</th> -->
                        <th colspan="2" class="border border-slate-300">Action</th>

                    </tr>
                    <tr v-for="(stud, i) in state.students" :key="stud">

                        <td class="border border-slate-300">{{ stud.student_id }}</td>
                        <td class="border border-slate-300">{{ stud.full_name }}</td>
                        <td class="border border-slate-300">{{ stud.email }}</td>
                        <td class="border border-slate-300">{{ stud.contact }}</td>
                        <!-- <td class="border border-slate-300">{{ stud.gender }}</td> -->
                        <td class="border border-slate-300">{{ stud.address }}</td>
                        <!-- <td class="border border-slate-300"> {{ state.subjectid }}</td> -->
                        <!-- <td class="border border-slate-300"><a>{{ stud.student_profile }}</a></td> -->
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
              " v-on:click="editFormValues(i)">
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
              " v-on:click="deleteFormValues(stud.student_id)">
                                Delete
                            </button>
                        </td>
                    </tr>

                </table>

            </div>
        </div>

    </div>
</template>


<script lang="ts">
import useVuelidate, {
    minLength,
    numeric,
    required,
    maxLength,
    email,
    alpha

} from '~/utils/vuelidate/useVuelidate';

export default {
    name: 'LoginPage',
};
</script>

<script setup lang="ts">

let state = reactive({
    students: [],
    filterArray: [],
    student: {
        student_id: null,
        full_name: null,
        email: null,
        contact: null,
        //  gender: null,
        // subjectid: null,
        address: null,
        // student_profile: null
    },
    subjects: [],
    subject_id: [],

    //  subjects: Array<string || number>,
});
var searchText = ''
/**
   * validation rules
   */
const rules = {
    full_name: { required, alpha, minLength: minLength(3) },
    email: { required, email },
    contact: { required, numeric, minLength: minLength(10), maxLength: maxLength(10) },
    address: { required },
    // subject: { required },
    // gender: { required }
};

/**
   * Search functionality
   */
function filteredRecords(searchText) {
    if (searchText) {
        var filtertable = state.students.filter(stud => stud.full_name.toLowerCase().includes(searchText.toLowerCase()))
        console.log(filtertable);
        state.students = filtertable;
    }
    else {
        state.students = state.filterArray
    }

}
//function call when we give any input to search 
function searchInput(evt) {
    console.log(evt);
    searchText = evt.target.value;
    console.log(searchText);
    filteredRecords(searchText);
}

const v$ = useVuelidate(rules, state.student);
var id: number;
var isEdit: boolean = false;
var studId: number;

getStudentsAPI();
// Get API
async function getStudentsAPI() {
    console.log("Get API call");
    // state.students = await $fetch('http://localhost:3001/student');
    state.filterArray = await $fetch('http://localhost:3001/student');
    state.students = state.filterArray;

}

getSubjectsAPI();
// Get API
async function getSubjectsAPI() {
    state.subjects = await $fetch('http://localhost:3001/subject');
    console.log(state.subjects);
}

// //post only subID
// async function submitSubId(id) {
//     console.log("dropdown click" + id);
//     // await $fetch('http://localhost:3002/studsub', {
//     //     method: 'POST',
//     //     body: JSON.stringify(id)
//     // });
// }

//PUT and POST API
async function submitFormValues() {
    // alert(state.student.student_id);
    console.log("submit click");
    const payload = state.student;
    console.log(payload);
    const studentId = payload.student_id;
    delete payload.student_id;
    if (isEdit === true) {
        const result = await v$.value.$validate();
        if (result) {
            alert("Invalid data info");
        }
        else {
            alert("store successfully");
        }
        await $fetch('http://localhost:3001/student/' + studentId, {
            method: 'PATCH',
            body: JSON.stringify(payload)
        }).then((res) => {
            alert("student information edited");
        });
        isEdit = false;
    } else {
        const result = await v$.value.$validate();
        if (result) {
            alert("data stored sucessfully");

        }
        else {
            alert("Invalid data");
        }
        await $fetch('http://localhost:3001/student', {
            method: 'POST',
            body: JSON.stringify(payload)
        }).then((res) => {
            console.log("id", res.student_id);
            studId = res.student_id;
            relationalTableValues();
        })

    }


    async function relationalTableValues() {
        console.log("studentId", studId);
        console.log(state.subject_id);
        state.subject_id.forEach((subid) => {
            const obj = {
                student: studId,
                subject: subid
            }
            var response = $fetch('http://localhost:3001/student/studsub', {
                method: 'POST',
                body: JSON.stringify(obj)
            }).then((res) => {
                console.log("data", obj);
                // studId = res.student_id;
            })
        })

    }

    getStudentsAPI();
    state.student = {
        student_id: '',
        full_name: '',
        email: '',
        contact: '',
        address: '',

        // student_profile: null
    }

}

async function editFormValues(i) {
    console.log(i);
    // let specificStudent = await $fetch('http://localhost:3002/student/' + i);

    state.student = Object.assign({}, state.students[i]);
    isEdit = true;

    // let specificStudent = await $fetch('http://localhost:3002/student/' + i);

    // // state.student = Object.assign({}, state.students[i]);
    // state.student.full_name = specificStudent.full_name;
    // state.student.email = specificStudent.email;
    // state.student.contact = specificStudent.contact;
    // state.student.address = specificStudent.address;

}

//DELETE API
async function deleteFormValues(index) {
    console.log(index);
    await $fetch('http://localhost:3001/student/' + index, {
        method: 'DELETE'
    });
    getStudentsAPI();
}



</script>





