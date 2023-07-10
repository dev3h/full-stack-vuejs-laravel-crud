<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <div class="alert alert-danger mt-4" v-if="errors.length">
          <ul class="mb-0">
            <li v-for="(error, index) in errors" :key="index">
              {{ index + 1 }}. {{ error }}
            </li>
          </ul>
        </div>

        <form @submit.prevent="storeContact">
          <fieldset>
            <div class="form-group">
              <label class="form-label mt-4">Name</label>
              <input
                type="text"
                v-model="formData.name"
                class="form-control"
                placeholder="enter name"
              />
            </div>
            <div class="form-group">
              <label class="form-label mt-4">Email</label>
              <input
                type="email"
                v-model="formData.email"
                class="form-control"
                placeholder="enter email"
              />
            </div>
            <div class="form-group">
              <label class="form-label mt-4">Designation</label>
              <input
                type="text"
                v-model="formData.designation"
                class="form-control"
                placeholder="enter designation"
              />
            </div>
            <div class="form-group">
              <label class="form-label mt-4">Contact no</label>
              <input
                type="text"
                v-model="formData.contact_no"
                class="form-control"
                placeholder="enter contact no"
              />
            </div>

            <button class="btn btn-primary mt-4">Create</button>
          </fieldset>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "AddContact",
  data() {
    return {
      formData: {
        name: "",
        email: "",
        designation: "",
        contact_no: "",
      },
      errors: [],
    };
  },
  methods: {
    async storeContact() {
      this.errors = [];
      if (!this.formData.name) {
        this.errors.push("Name is required");
      }
      if (!this.formData.email) {
        this.errors.push("Email is required");
      }
      if (!this.formData.designation) {
        this.errors.push("Designation is required");
      }
      if (!this.formData.contact_no) {
        this.errors.push("Contact No is required");
      }

      if (!this.errors.length) {
        let url = "http://127.0.0.1:8000/api/contacts/";
        try {
          let response = await axios.post(url, this.formData);
          console.log("data", response?.data?.message);
          if (response?.status == 200) {
            this.formData = {
              name: "",
              email: "",
              designation: "",
              contact_no: "",
            };
            alert(response?.data?.message);
          }
        } catch (error) {
          console.log(error);
        }
      }
    },
  },
};
</script>
