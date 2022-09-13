<template>
  <td class="py-[12px]"><input type="checkbox" /></td>
  <td class="py-[12px] pl-[10px]">{{ name }}</td>
  <td class="py-[12px] pl-[10px]">{{ person.email }}</td>
  <td class="py-[12px] pl-[10px]">{{ person.address.address || person.address }}</td>
  <td class="py-[12px] pl-[10px]">{{ person.phone }}</td>
  <td class="py-[12px] pl-[10px]">
    <button @click="editUser">
      <i class="fa-solid fa-pen text-yellow-300 mr-5"></i>
      <div
        v-if="isShowEdit"
        class="fixed bg-black/[0.3] top-0 left-0 w-full h-full"
      >
        <form
          class="absolute top-[50%] left-[50%] translate-y-[-50%] translate-x-[-50%] bg-white text-black p-4"
        >
          <h3 class="font-bold">Edit Employee</h3>
          <label for="">Name</label><br />
          <input
            v-model="modelName"
            class="border-2"
            type="text"
            placeholder="Enter name"
          /><br />
          <label for="">Email</label><br />
          <input
            v-model="modelEmail"
            class="border-2"
            type="text"
            placeholder="Enter email"
          /><br />
          <label for="">Address</label><br />
          <input
            v-model="modelAddress"
            class="border-2"
            type="text"
            placeholder="Enter address"
          /><br />
          <label for="">Phone</label><br />
          <input
            v-model="modelPhone"
            class="border-2"
            type="text"
            placeholder="Enter phone"
          /><br />
          <div class="flex justify-end mt-3">
            <button class="bg-yellow-300 p-1 mr-2 rounded" type="">
              Cancel
            </button>
            <button
              class="bg-green-500 p-1 rounded"
              type="button"
              @click="saveNewUser(person.id)"
            >
              Save
            </button>
          </div>
        </form>
      </div>
      <div v-else></div>
    </button>
    <button @click="deleteUser">
      <i class="fa-solid fa-trash text-red-500"></i>
      <div
        v-if="isShowDel"
        class="fixed bg-black/[0.3] top-0 left-0 w-full h-full"
      >
        <div
          class="absolute top-[50%] left-[50%] translate-y-[-50%] translate-x-[-50%] bg-white text-black p-4"
        >
          <h3 class="font-bold">Delete Employee</h3>
          <p>Are you sure you want to delete these Records?</p>
          <div class="flex justify-end mt-3">
            <button class="bg-yellow-300 p-1 mr-2 rounded" type="">
              Cancel
            </button>
            <button
              @click="deleteMethod(person.id)"
              class="bg-red-500 p-1 rounded"
              type="submit"
            >
              Delete
            </button>
          </div>
        </div>
      </div>
      <div v-else></div>
    </button>
  </td>
</template>
<script>
import axios from "axios";
export default {
  props: {
    person: Object,
  },
  computed: {
    name() {
      return (
        this.person.name || this.person.firstName + " " + this.person.lastName
      );
    },
  },
  data() {
    return {
      isShow: false,
      isShowEdit: false,
      isShowDel: false,

      modelName: "",
      modelEmail: "",
      modelAddress: "",
      modelPhone: "",
      // persons: {
      //   id: "",
      //   name: "",
      //   email: "",
      //   address: "",
      //   phone: ""
      // }
    };
  },
  methods: {
    editUser() {
      // event.stopPropagation()
      console.log("sua het");
      this.isShowEdit = true;
    },
    deleteUser() {
      console.log("xoa het");
      this.isShowDel = !this.isShowDel;
    },
    saveNewUser(userId) {
      axios.put(`https://dummyjson.com/users/${userId}`).then((res) => {
        const editUser = {
          id: userId,
          name: this.modelName,
          email: this.modelEmail,
          address: this.modelAddress,
          phone: this.modelPhone,
        };
        this.$emit("passEditId", editUser);
      });
    },
    deleteMethod(userId) {
      console.log(userId);
      axios.delete(`https://dummyjson.com/users/${userId}`).then((res) => {
        this.$emit("passId", userId);
      });
    },
  },
};
</script>
<style></style>
