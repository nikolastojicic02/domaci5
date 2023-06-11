<template>
    <div>
      <h2>Edit Employee</h2>
      <form @submit.prevent="updateEmployee">
        <label for="firstName">First Name:</label>
        <input type="text" id="firstName" v-model="employee.firstName" required>
  
        <label for="lastName">Last Name:</label>
        <input type="text" id="lastName" v-model="employee.lastName" required>
  
        <label for="position">Position:</label>
        <input type="text" id="position" v-model="employee.position" required>
  
        <button type="submit">Update</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    name: "EditEmployeeView",
    data() {
      return {
        employee: {
          firstName: "",
          lastName: "",
          position: ""
        }
      };
    },
    mounted() {
      this.fetchEmployee();
    },
    methods: {
      fetchEmployee() {
        const employeeId = this.$route.query.id;
        axios
          .get(`http://localhost:8081/api/employees/${employeeId}`)
          .then((response) => {
            this.employee = response.data;
          })
          .catch((error) => {
            console.error(error);
          });
      },
      updateEmployee() {
        const employeeId = this.$route.query.id;
        axios
          .put(`http://localhost:8081/api/employees/${employeeId}`, this.employee)
          .then((response) => {
            console.log(response);
            // Handle success, such as showing a success message or redirecting to another page
            this.$router.push("/employees");
          })
          .catch((error) => {
            console.error(error);
            // Handle error, such as showing an error message
            alert("Something went wrong!");
          });
      }
    }
  };
  </script>
  
  <style scoped>
  </style>