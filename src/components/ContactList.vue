<template>
  <div class="container">
    <table class="table table-hover">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Designation</th>
          <th scope="col">Contact No</th>
        </tr>
      </thead>
      <tbody v-for="contact in contacts" :key="contact?.id">
        <tr class="table-second">
          <td scope="row">{{ contact?.id }}</td>
          <td>{{ contact?.name }}</td>
          <td>{{ contact?.email }}</td>
          <td>{{ contact?.designation }}</td>
          <td>{{ contact?.contact_no }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "ContactList",
  data() {
    return {
      contacts: Array,
    };
  },
  created() {
    this.getContacts();
  },
  methods: {
    async getContacts() {
      let url = "http://127.0.0.1:8000/api/contacts/";
      try {
        let response = await axios.get(url);
        if (response?.status == 200) {
          this.contacts = response?.data?.contacts;
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
  mounted() {
    console.log("Component mounted.");
  },
};
</script>
