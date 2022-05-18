<template>
  <div>
    <h1 class="text-center">
      Project Management Evaluation<span class="smaller">BY HMI GROUP 3</span>
    </h1>
  </div>
  <div class="container">
    <!-- Show Add Student Button-->
    <div class="col-lg-12">
      <button class="float-end btn btn-info" @click="addModalDialog(true)">
        <FIcons :icon="['fas', 'user']" /> Add New Student
      </button>
      <button class="float-start btn btn-danger" v-if="studentsData.length > 0">
        <FIcons :icon="['fas', 'user']" /> Delete All Students
      </button>
      <div class="clearfix"></div>
    </div>
    <hr class="bg-info" />

    <!-- Show Error Message-->
    <!-- Show Success Message-->
    <div
      class="alert alert-danger alert-dismissible fade show"
      role="alert"
      v-if="errMsg"
    >
      {{ errMsg }}
      <button
        type="button"
        class="btn-close"
        data-bs-dismiss="alert"
        aria-label="close"
      ></button>
    </div>
    <div
      class="alert alert-success alert-dismissible fade show"
      role="alert"
      v-if="successMsg"
    >
      {{ SuccessMsg }}
      <button
        type="button"
        class="btn-close"
        data-bs-dismiss="alert"
        aria-label="close"
      ></button
      >C
    </div>
    <!-- Show Add Students  Details : Tables-->
    <table class="table table-border table-striped caption-top">
      <caption>
        Records of the students ({{
          studentsData.length
        }})
      </caption>
      <thead>
        <tr class="bg-success text-light text-center">
          <th><FIcons :icon="['fas', 'id-badge']" /> ID</th>
          <th><FIcons :icon="['fas', 'user']" /> Name</th>
          <th><FIcons :icon="['fas', 'envelope']" /> Email</th>
          <th><FIcons :icon="['fas', 'phone']" /> phone</th>
          <th><FIcons :icon="['fas', 'cog']" /> Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr class="text-center">
          <td>1</td>
          <td>John Smith</td>
          <td>smith@gmail.com</td>
          <td>0196754367</td>
          <td>
            <button class="btn btn-danger">
              <FIcons :icons="['fas', 'user-timer']" />Delete
            </button>
            &nbsp;
            <button class="btn btn-warning">
              <FIcons :icons="['fas', 'user-edit']" />update
            </button>
          </td>
        </tr>
        <tr class="text-center">
          <td>1</td>
          <td>John Smith</td>
          <td>smith@gmail.com</td>
          <td>0196754367</td>
          <td>
            <button class="btn btn-danger">
              <FIcons :icons="['fas', 'user-timer']" />Delete
            </button>
            &nbsp;
            <button class="btn btn-warning">
              <FIcons :icons="['fas', 'user-edit']" />update
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <!-- Show Add New Student Modal-->
    <div id="overlay" v-if="showAddModal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="model-title text-info">Add New User</h5>
            <button aria-hidden="true" @click="addModalDialog(false)">
              <FIcons :icon="['fas', 'times']" />
            </button>
          </div>
          <div class="modal-body p-4">
            <form action="#" method="post" @click.prevent>
              <div
                class="form-floating mb-3"
                :class="{ 'form-group-error': v$.newStudent.name.$error }"
              >
                <input
                  type="text"
                  class="form-control"
                  id="studentNameFloat"
                  placeholder="John Ken"
                  v-model="newStudent.name"
                />
                <label for="studentNameFloat"
                  ><FIcons :icon="['far', 'user']" />Student Name</label
                >
                <span class="error-feedback" v-if="v$.newStudent.name.$error">
                  {{ v$.newStudent.name.$error[0].$message }}
                </span>
              </div>
              <div
                class="form-floating mb-3"
                :class="{ 'form-group-error': v$.newStudent.email.$error }"
              >
                <input
                  type="email"
                  class="form-control"
                  id="studentEmailFloat"
                  placeholder="John Ken"
                  v-model="newStudent.email"
                />
                <label for="studentEmailFloat"
                  ><FIcons :icon="['far', 'envelope']" />Student Email</label
                >
                <span class="error-feedback" v-if="v$.newStudent.email.$error">
                  {{ v$.newStudent.email.$error[0].$message }}
                </span>
              </div>
              <div
                class="form-floating mb-3"
                :class="{ 'form-group-error': v$.newStudent.phone.$error }"
              >
                <input
                  type="tel"
                  class="form-control"
                  id="studentPhoneFloat"
                  placeholder="John Ken"
                  v-model="newStudent.phone"
                />
                <label for="studentPhoneFloat"
                  ><FIcons :icon="['fas', 'phone']" />Student Phone</label
                >
                <span class="error-feedback" v-if="v$.newStudent.phone.$error">
                  {{ v$.newStudent.phone.$error[0].$message }}
                </span>
              </div>
              <hr class="bg-info" />
              <div class="d-grid gap-2">
                <button class="btn btn-info" @click="addNewUser()">
                  Add New User
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
    <!-- Show Edit Student Modal-->
    <!-- Show Delete Student Modal-->
    <!-- Show Delete All Students Modal-->
  </div>
</template>

<script>
import useValidate from "@vuelidate/core";
import { required, email, minLength } from "@vuelidate/validators";
export default {
  name: "RegisterUsers",
  data() {
    return {
      v$: useValidate(),
      errMsg: "",
      successMsg: "",
      studentsData: [],
      showAddModal: false,
      newStudent: {
        name: "",
        email: "",
        phone: "",
      },
    };
  },
  validations() {
    return {
      newStudent: {
        name: { required, minLength: minLength(3) },
        email: { required, email },
        phone: { required, minLength: minLength(10) },
      },
    };
  },
  methods: {
    addModalDialog(val) {
      this.showAddModal = val;
    },
    addNewUser() {
      this.v$.newStudent.$useValidate();
      if (!this.v$.newStudent.$error) {
        console.log("Add New User : Validated Successfully");
      } else {
        console.log("Add New User not Validated ");
      }
    },
  },
};
</script>

<style scoped>
h1 {
  background-color: cadetblue;
  color: white;
  padding: 8px;
  margin-top: 0;
  margin-bottom: 50px;
}
.smaller {
  font-size: 0.85rem;
}
#overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgb(0 0 0 / 47%);
}
.form-group-error {
  color: red;
}
.form-group-error input {
  border-color: red;
}
</style>
