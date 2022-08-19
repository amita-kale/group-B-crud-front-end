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

                </form>
            </div>
            <div class="bg-gray-300 col-span-2">hello

            </div>
        </div>
    </div>
</template>