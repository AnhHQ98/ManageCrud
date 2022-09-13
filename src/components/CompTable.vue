<template>
  
    <table class="container mx-auto mt-1">
      {{
        log(people)
      }}
      <thead>
        <tr class="border-y-4">
          <th class="py-[12px]"><input type="checkbox" /></th>
          <th class="py-[12px]">Name</th>
          <th class="py-[12px]">Email</th>
          <th class="py-[12px]">Address</th>
          <th class="py-[12px]">Phone</th>
          <th class="py-[12px]">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr class="border-b-2" v-for="(person, index) in people" :key="index">
          <CompPage
            :person="person"
            v-if="
              10 * (currentPage - 1) < person.id &&
              person.id <= 10 * currentPage
            "
            @passId="receiveId"
            @passEditId="receiveEditId"
          />
        </tr>
      </tbody>
    </table>
    <div class="flex justify-end pr-14 my-6">
      <div v-for="i in totalPage" :key="i">
        <button
          @click="currentPage = i"
          class="bg-green-200 hover:bg-green-600 hover:text-white py-1 px-3 mx-1 rounded-full"
        >
          {{ i }}
        </button>
      </div>
    </div>
  
</template>
<script>
import CompPage from "./CompPage.vue";
export default {
  components: {
    CompPage,
  },
  props: ["data"],
  data() {
    return {
      currentPage: 1,
      totalPage: 1,
    };
  },
  props: {
    people: {
      type: Object,
    },
  },
  methods: {
    log(msg) {
      console.log(msg);
    },
    receiveId(deleteId) {
      this.$emit("passId", deleteId);
    },
    receiveEditId(editUser_2) {
      this.$emit("passEditId", editUser_2);
    },
  },
  // watch:{
  //     data(){
  //       this.data.id=this.people.length+1
  //       console.log(this.data);
  //     }
  // },
  computed: {
    totalPage() {
      console.log(this.people.length);
      if (this.people.length > 0) {
        if (this.people.length % 10 == 0) {
          return parseInt(this.people.length / 10);
        }
        return parseInt(this.people.length / 10) + 1;
      } else return 1;
    },
  },
};
</script>
<style></style>
