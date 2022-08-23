<template>
<div>
    <title>
        Book Management System
    </title>
    <h1 class="text-center font-extrabold text-5xl mt-4 bg-blue-300">Book Management System Welcomes You !!</h1>
    <hr class="mt-5 border-1 border-black">
    <!-- import MyComp from "@/components/MyComp.vue"; -->
    <div class="sm  border-4 bg-gray-100 mr-60 ml-60 p-4 border-solid border-black rounded-md mt-6 ">
        <form action="" name="myForm" onsubmit="return validateForm()" method="post" >
            <!-- <div class="justify-between p-1 sm">
                <label class="font-semibold text-xl mr-16" for="bookid">Book ID</label>
                <input class="ml-16 border-2 px-32" type="number" v-model="formdata.bookid" name="bookid" id="bookid" @change="validationBookid" required>
            </div> -->
            <div class="justify-between p-1 sm">
                <label class="font-semibold text-xl mr-16" for="bookname">Book Name</label>
                <input class="ml-16 border-2 px-32" type="text" v-model="formdata.bookname" name="bookname" id="bookname" @change="validationName" required>
            </div>
            <div class="p-1">
                <label class="font-semibold text-xl mr-16" for="bookauthor">Book Author</label>
                <input class="ml-16  border-2 px-32 " type="text" v-model="formdata.bookauthor" name="bookauthor" id="bookauthor" @change="validationAuthor" required>
            </div>
            <div class="p-1">
                <label class="font-semibold text-xl mr-16" for="bookprice">Book Price</label>
                <input class="ml-8 border-2 px-32" type="number" v-model="formdata.bookprice" name="bookprice" id="bookprice" @change="validationPrice" required>
            </div>
            <div class="p-1">
                <label class="font-semibold text-xl mr-16" for="bookimage">Book Image</label>
                <input class="ml-16 border-2 px-32" type="text" v-model="formdata.bookimage" name="bookimage" id="bookimage" @change="validationImage" required>
            </div>
            <div class="p-1">
                <label class="font-semibold text-xl mr-16" for="bookisbn">Book ISbn No.</label>
                <input class="ml-16 border-2 px-32" type="number" v-model="formdata.bookisbn" name="bookisbn" id="bookisbn" @change="validationBookisbn" required>
            </div>
            <div class="p-1  mt-6">
                <button class="ml-16 border-2 font-bold mr-16 rounded-md bg-black text-blue-500 hover:bg-black hover: text-white p-2 text-center" type="submit" @click="addpro">Add Book</button>
                <button class="ml-16 border-2 font-bold mr-16 rounded-md bg-black text-blue-500 hover:bg-black  text-white p-2 text-center" type="reset">Reset</button>
            </div>
        </form>
        <table border="2" class="border-2  bg-gray-100 mr-60 ml-32 p-6 border-solid border-black rounded-md mt-8 ">
            <tr>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book ID</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book Name </td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book Author</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book Price</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book Image</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book ISbn No.</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Delete</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Edit Data</td>
            </tr>
            <tr v-for="(item,i) in myarr" :key="item">
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{item.bookid = i + 1}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{item.bookname}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{item.bookauthor}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{item.bookprice}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{item.bookimage}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{item.bookisbn}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8"><button class=" border-2 font-bold rounded-md bg-green-500 hover:bg-black  text-white p-2 text-center" @click="deletepro(i)">Delete</button></td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8"><button class=" border-2 font-bold rounded-md bg-green-500 hover:bg-black  text-white p-2 text-center" @click="editpro(i)">Edit</button></td>
            </tr>
        </table>
        <div >
            <label class="font-bold text-xl mr-16" for="searchpro">Search Books</label>
            <input @keyup="userFindByAddress(userAddress)" v-model="this.userAddress" class="ml-2 mt-8 border-2 px-32" type="text" name="searchpro" id="searchpro">
            <!-- <button class=" border-2 font-bold rounded-md bg-red-300 text-blue-500 hover:bg-black  text-white p-2 text-center" type="search" @click="this.userFindByAddress(userAddress)">Search</button> -->
        </div>
        <hr class="border-1 border-black">
        <!-- 2nd table  -->
        <table border="2" class="border-2  bg-gray-100 mr-60 ml-32 p-6 border-solid border-black rounded-md mt-8 ">
            <tr>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book ID</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book Name</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book Author</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book Price</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book Image</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Book ISbn No.</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Delete Book</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8 font-bold">Edit Book</td>
            </tr>
            <tr v-for="(prod,i) in userFound" :key="prod">
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{prod.bookid = i + 1}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{prod.bookname}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{prod.bookauthor}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{prod.bookprice}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{prod.bookimage}}</td>
                <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8">{{prod.bookisbn}}</td>
                <!-- <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8"><button class=" border-2 font-bold rounded-md bg-red-300 text-blue-500 hover:bg-black  text-white p-2 text-center" @click="deletepro(i)">Delete Product</button></td> -->
                <!-- <td class="border-2  bg-gray-100 p-2 border-solid border-black rounded-md mt-8"><button class=" border-2 font-bold rounded-md bg-red-300 text-blue-500 hover:bg-black  text-white p-2 text-center" @click="editpro(i)">Edit</button></td> -->
            </tr>
        </table>
    </div>
</div>
</template>

<script>
export default {
    name: "product-data",
    data() {
        return {
            isEdit: false,
            indexEdit: -1,
            userAddress: "",
            myarr: [],
            formdata: {
                bookid: 0,
                bookname: "",
                bookauthor: "",
                bookprice: "",
                bookimage: "",
                bookisbn: "",
            }
        }
    },
    methods: {
        addpro(event) {
            event.preventDefault();
            //validation bookname
            if( !isNaN(this.formdata.bookname) || this.formdata.bookname==null || this.formdata.bookname==""){
                    alert("Please Enter Book Name");
                    // console.log("Please Enter Name");
                    this.resetForm();
            }else{
                console.log(this.formdata.bookname);
                    alert("Book Name is valid ...!!!");
            }
            // //vali author
             if( !isNaN(this.formdata.bookauthor) || this.formdata.bookauthor=="" || this.formdata.bookauthor==null ){
            // if( !isNaN(this.formdata.price) || !this.formdata.price==null || !this.formdata.price==""  ){
                // || this.formdata.price==""
                    alert("Please Enter Book Author");
                    // console.log("Please Enter price");
                    this.resetForm();
            }else{
                console.log(this.formdata.bookauthor);
                    alert("Book Author is valid");
            }
            //vali Price
            if( isNaN(this.formdata.bookprice) || this.formdata.bookprice==null || this.formdata.bookprice==""){
                    alert("Please Enter bookprice");
                    // console.log("Please Enter bookprice");
                    this.resetForm();
            }else{
                console.log(this.formdata.bookprice);
                     alert("categoy is valid");
            }
            //vali Image
            if( !isNaN(this.formdata.bookimage) || this.formdata.bookimage==null || this.formdata.bookimage==""){
                    alert("Please Enter bookimage");
                    // console.log("Please Enter bookimage");
                    this.resetForm();
            }else{
                console.log(this.formdata.bookimage);
                     alert("Book Name is Image");
            }
            //vali Isbn no
            if( isNaN(this.formdata.bookisbn || this.formdata.bookisbn==null || this.formdata.bookisbn=="")){
                    alert("Please Enter bookisbn no");
                    // console.log("Please Enter bookimage");
                    this.resetForm();
            }else{
                console.log(this.formdata.bookisbn);
                     alert("Book isbn no is valid");
            }
            //other if else condition
            if (this.isEdit == true) {
                this.myarr[this.indexEdit] = this.formdata;
                this.isEdit = false;
                this.indexEdit = -1;
            } else {
                this.myarr.push(this.formdata);
            }
            this.formdata = {
                bookid: 0,
                bookname: "",
                bookauthor: "",
                bookprice: "",
                bookimage: "",
                bookisbn: "",
            }
            console.log("Formdata is :", this.myarr);
        },
        deletepro(index) {
            this.myarr.splice(index, 1);
        },
        editpro(index) {
            this.formdata.bookid = this.myarr[index].bookid;
            this.formdata.bookname = this.myarr[index].bookname;
            this.formdata.bookauthor = this.myarr[index].bookauthor;
            this.formdata.bookprice = this.myarr[index].bookprice;
            this.formdata.bookimage = this.myarr[index].bookimage;
            this.formdata.bookisbn = this.myarr[index].bookisbn;
            this.isEdit = true;
            this.indexEdit = index;
        },
        userpro(userName) {
            // user1 = this.userName
            // if(this.allUserData.filter(e => e.firstName == userName})){
            //     alert("user Found" + e.firstName+ ""+e.lastName);
            // }
            console.log(userName);
            this.userFound = this.myarr.filter((e) => {
                if (e.bookname == userName) {
                    // this.userFound.push(e);
                    console.log(e);
                    return e;
                    // alert("user Found" + e.firstName+ ""+e.lastName);
                }
                // else{
                // alert("user not found");
                // }
                // console.log(this.userFind);
            });
            // console.log(find1);
            console.log(this.userFound);
        },
        userFindByAddress(userAddress) {
            // console.log(userAddress);
            this.userFound = this.myarr.filter((e) => {
                // if (e.pname == userAddress)
                // this.bookid1 = userAddress.toString();
                // this.bookid2 = e.category.toString();
                this.bookname1 = userAddress.toLocaleLowerCase();
                this.bookname2 = e.bookname.toLocaleLowerCase();
                this.bookauthor1 = userAddress.toLocaleLowerCase();
                this.bookauthor2 = e.bookauthor.toLocaleLowerCase();
                this.bookprice1 = userAddress.toString();
                this.bookprice2 = e.bookprice.toString();
                this.bookimage1 = userAddress.toLocaleLowerCase();
                this.bookimage2 = e.bookimage.toLocaleLowerCase();
                this.bookisbn1 = userAddress.toString();
                this.bookisbn2 = e.bookisbn.toString();
                if (this.bookname2.startsWith(this.bookname1) || this.bookauthor2.startsWith(this.bookauthor1) || this.bookprice2.startsWith(this.bookprice1) || this.bookimage2.startsWith(this.bookimage1) || this.bookisbn2.startsWith(this.bookisbn1)) {
                    console.log(e);
                    return e;
                }
            });
            console.log(this.userFound);
        },
    }
}
</script>