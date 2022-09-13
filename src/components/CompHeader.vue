<template>
  <div class="relative header container mx-auto bg-[#435d7d] text-white py-[16px] px-[30px] flex justify-between items-center">
    <h2 class="text-2xl text-white">Manage <b>Employees</b></h2>
    <div class="header__button">
      <button class="bg-red-500 hover:bg-red-600 py-[5px] px-[12px] mr-[10px] rounded">
        <i class="fa-solid fa-circle-minus mr-1"></i>Delete
      </button>
      <button @click="addNewUser" class="bg-green-600 hover:bg-green-700 py-[5px] px-[12px] rounded">
        <i class="fa-solid fa-circle-plus mr-1"></i>Add New Employee
      </button>
      <div v-if="isShow" class="fixed bg-black/[0.3] top-0 left-0 w-full h-full">
        <form class="absolute top-[50%] left-[50%] translate-y-[-50%] translate-x-[-50%] bg-white text-black p-10">
          <h3 class="font-bold">Add New Employee</h3>
          <label for="">Name</label><br>
          <input class="border-2" type="text" placeholder="Enter name" v-model="newUser.name"><br>
          <label for="">Email</label><br>
          <input class="border-2" type="text" placeholder="Enter email" v-model="newUser.email"><br>
          <label for="">Address</label><br>
          <input class="border-2" type="text" placeholder="Enter address" v-model="newUser.address"><br>
          <label for="">Phone</label><br>
          <input class="border-2" type="text" placeholder="Enter phone" v-model="newUser.phone"><br>
          <div class="flex justify-end mt-3">
            <button class="bg-yellow-300 p-1 mr-2 rounded" >Cancel</button>
            <button class="bg-green-500 p-1 rounded" type="button" @click="saveNewUser">Save</button>
          </div>
        </form>
      </div>
      <div v-else></div>
    </div> 
  </div>
</template>
<script>
export default{
  data(){
    return{
      isShow: false,
      newUser:{
        id:'',
        name:'',
        address:'',
        email:'',
        phone:'',
      }
    }
  },
  methods: {
    addNewUser(){
      this.isShow = !this.isShow
    },
    addNewUserCancel(){
      this.isShow = false
    },
    saveNewUser(event){
        this.$emit("receiveUser", {...this.newUser})
        event.preventDefault();
       this.isShow = !this.isShow
       this.newUser.name=""
       this.newUser.address=""
       this.newUser.email=""
       this.newUser.phone=""
    }, 
  }
}
</script>
<style>

</style>