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
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"></td>
                        </tr>
                        <tr>
                            <td><label>Email :</label></td>
                            <td><input type="email"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"></td>
                        </tr>
                        <tr>
                            <td><label>Contact</label></td>
                            <td><input type="number"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"></td>
                        </tr>
                        <tr>
                            <td><label>Address</label></td>
                            <td><textarea
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-9 pr-4 ml-2 mb-2"></textarea>
                            </td>
                        </tr>
                        <tr>
                            <td><label>Student Profile:</label></td>
                            <td><input type="file"
                                    class="bg-white border border-slate-300 rounded-md py-2 pl-2 pr-2 ml-2 mb-2 w-52">
                            </td>
                        </tr>
                    </table>
                    <button type="button" class="border-solid rounded border-2 border-indigo-600 p-3 ml-36 mt-3
                bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500">Submit</button>
                </form>
            </div>
            <div class="bg-gray-300 col-span-2">

                <input
                    class="placeholder:italic placeholder:text-slate-400 block bg-white w-50 border border-slate-300 rounded-md m-10 py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm"
                    placeholder="Search for anything..." type="text" name="search" />
                <table class=" border-black-400 border-separate bg-white  border border-slate-400 m-20">
                    <tr>
                        <th>StudentID</th>
                        <th>FullName</th>
                        <th>Email</th>
                        <th>Contact</th>
                        <th>Address</th>
                        <th>StudentProfile</th>
                        <th colspan="2">Action</th>
                    </tr>

                </table>

            </div>
        </div>
    </div>
</template>