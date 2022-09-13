<template>
  <CompHeader @receiveUser="receive" />
  <CompTable :people="people" @passId="receiveId" @passEditId="passEditId" />
</template>
<script>
import CompHeader from "./components/CompHeader.vue";
import CompTable from "./components/CompTable.vue";
import axios from "axios";
export default {
  components: {
    CompHeader,
    CompTable
  },
  data() {
    return {
      newUserApp: {},
      people: [],
    };
  },
  created() {
    this.getUser();
  },
  methods: {
    receive(data) {
      // console.log(data)
      this.people.push({ ...data, id: this.people.length + 1 });
      // console.log(this.people)
    },
    receiveId(deleteId) {
      console.log(deleteId);
      this.people.splice(deleteId - 1, 1);
    },
    resetData() {
      this.newUserApp = {};
    },
    async getUser() {
      const res = await axios.get("https://dummyjson.com/users");
      this.people = [...res.data.users];
    },
    passEditId(editUser_3) {
      console.log(editUser_3);
      // for (user in editUser_3) {
      //   if (people.id == editUser_3.id){
      //     editUser_3 == people;
      //   }
      // }
      // editUser_3 = this.people.findIndex((obj => editUser_3 == people.id));
      // vong for xong if id phan tu = id truyen vao thi cho phan tu = cais truyen vao
    },
  },
};
</script>
<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>