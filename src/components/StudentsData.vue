<template>
<div id="app">
<div class="row">
    <div class="col-sm-12">
      <!-- Modal for delete -->
      <div class="modal fade" id="create-student" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLongTitle">Create Student Form</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <div class="card bg-light">
                  <!-- <div class="card-header">
                  Student Initial Details
                  </div> -->
                  <div class="card-body">
                  <h3 class="card-title">Initial Details</h3>
                  <hr>
                  <form @submit.prevent="submitForm">
                      <div class="form-group">
                      <label for="firstName">First Name</label>
                      <input type="text" class="form-control" placeholder="First Name" v-model="student.first_name" required='required'>
                      </div>
                      <div class="form-group">
                      <label for="lastName">Last Name</label>
                      <input type="text" class="form-control" placeholder="Last Name" v-model="student.last_name" required='required'>
                      </div>
                      <div class="form-group">
                      <label for="middleName">Middle Name</label>
                      <input type="text" class="form-control" placeholder="Middle Name" v-model="student.middle_name">
                      </div>
                      <div class="form-group">
                      <label for="extensionName">Extension Name</label>
                      <input type="text" class="form-control" placeholder="Extension Name" v-model="student.extension_name">
                      </div>
                      <div class="form-group">
                      <label for="birthDate">Birth Date</label>
                      <input type="date" class="form-control" placeholder="Birth Date" v-model="student.birth_date" required='required'>
                      </div>
                      <div class="form-group">
                      <label for="parentContact">Parent Mobile Contact</label>
                      <input type="text" class="form-control" placeholder="Parent Contact" v-model="student.parent_contact" required='required'>
                      </div>
                      <div class="form-group">
                      <label for="parentEmail">Parent Email Address</label>
                      <input type="email" class="form-control" placeholder="Parent Email" v-model="student.parent_email">
                      </div>
                      <!-- <input type="hidden" id="postId" name="user" v-model="student.user" value=""> -->
                      <button class="btn btn-outline-primary btn-sm">Submit</button>
                      <a class="btn float-right" style="color: red;" @click="clearList">Clear</a>
                  </form>
                  </div>
              </div>
            </div>
            <!-- <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            </div> -->
          </div>
        </div>
      </div>
      <!-- Modal for details -->
      <div class="modal fade" id="student-details" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLongTitle">Student Details</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
                <strong>{{ student.get_fullname }}</strong>
                <br>
                <small class="text-muted">Date Register: {{ student.date_register|formatDate }}</small>
                <hr>
                <!-- <button type="button" class="btn btn-outline-danger btn-sm" @click="deleteStudent(student)"><i class="fas fa-trash-alt"></i></button> -->
            </div>
            <!-- <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            </div> -->
          </div>
        </div>
      </div>
      <div class="modal fade" id="edit-student" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLongTitle">Student Details</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
                <div class="card bg-light">
                    <!-- <div class="card-header">
                    Student Initial Details
                    </div> -->
                    <div class="card-body">
                    <h3 class="card-title">Edit Students</h3>
                    <hr>
                    <form @submit.prevent="submitForm">
                        <div class="form-group">
                        <label for="firstName">First Name</label>
                        <input type="text" class="form-control" placeholder="First Name" v-model="student.first_name" required='required'>
                        </div>
                        <div class="form-group">
                        <label for="lastName">Last Name</label>
                        <input type="text" class="form-control" placeholder="Last Name" v-model="student.last_name" required='required'>
                        </div>
                        <div class="form-group">
                        <label for="middleName">Middle Name</label>
                        <input type="text" class="form-control" placeholder="Middle Name" v-model="student.middle_name">
                        </div>
                        <div class="form-group">
                        <label for="extensionName">Extension Name</label>
                        <input type="text" class="form-control" placeholder="Extension Name" v-model="student.extension_name">
                        </div>
                        <div class="form-group">
                        <label for="birthDate">Birth Date</label>
                        <input type="date" class="form-control" placeholder="Birth Date" v-model="student.birth_date" required='required'>
                        </div>
                        <div class="form-group">
                        <label for="parentContact">Parent Mobile Contact</label>
                        <input type="text" class="form-control" placeholder="Parent Contact" v-model="student.parent_contact" required='required'>
                        </div>
                        <div class="form-group">
                        <label for="parentEmail">Parent Email Address</label>
                        <input type="email" class="form-control" placeholder="Parent Email" v-model="student.parent_email">
                        </div>
                        <!-- <input type="hidden" id="postId" name="user" v-model="student.user" value=""> -->
                        <button class="btn btn-outline-primary btn-sm">Update</button>
                        <!-- <a class="btn float-right" style="color: red;" @click="deleteStudent(student)"><i class="fas fa-trash-alt"></i></a> -->
                    </form>
                    </div>
                </div>
            </div>
            <!-- <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            </div> -->
          </div>
        </div>
      </div>
    <div class="card">
        <div class="card-body">
        <h3 class="card-title">Student list <button type="button" name="button" class="btn btn-outline-primary btn-sm float-right" data-toggle="modal" data-target="#create-student">Add</button></h3>
        <input class="form-control mr-sm-2" v-model="search" type="search" placeholder="Search Student" aria-label="Search">
        <hr>
        <p class="text-muted">Filters | </p>
        <table class="table table-sm table-hover">
            <thead>
            <tr>
                <th>Full Name</th>
                <th>Parent Contact</th>
                <th>Settings</th>
            </tr>
            </thead>
            <tbody v-for="student in studentlist" :key="student.id">
            <tr v-for="stud in student.results" :key="stud.id" @dblclick="$data.student = stud">
                <!-- <td>{{student.first_name}}</td> -->
                <td>
                <strong>{{stud.last_name}}, {{stud.first_name}}</strong>
                <br>
                <small class="text-muted">Date registered: {{stud.date_register|formatDate}} | Created by: {{ stud.user }}</small>
                </td>
                <td>{{stud.parent_contact}}</td>
                <td>
                <button class="btn btn-outline-info dropdown-toggle btn-sm float-left" type="button" id="dropdownMenu2" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
    <i class="fas fa-cog"></i>
  </button>
  <div class="dropdown-menu" aria-labelledby="dropdownMenu2">
    <button class="dropdown-item" type="button" data-toggle="modal" data-target="#student-details" :key="stud.id" @click="$data.student = stud">Details</button>
    <button class="dropdown-item" type="button" data-toggle="modal" data-target="#edit-student" :key="stud.id" @click="$data.student = stud">Edit</button>
    <button class="dropdown-item" type="button" style="color: red;" @click="deleteStudent(stud)">Delete</button>
  </div>
                </td>
            </tr>
            </tbody>
        </table>
        </div>
    </div>
    </div>
</div>
</div>
</template>

<script>
import Vue from 'vue';
import Axios from 'axios';
import VueAxios from 'vue-axios'
Vue.use(VueAxios,Axios)
const access_token = '69f1961880f7484b415e08ea0e0397725c4a904a'
// const access_token = 'afcf65f4f24537fee9dd69119127c974840ae0cf' // local token
// var localserve = 'http://localhost:8000/students'
// http://franky88.pythonanywhere.com/students/?format=json
export default {
    name: "StudentsData",
    data(){
        return {
            student: {},
            studentlist: []
        }
    },
    async created() {
        this.getStudents();
    },
    methods: {
        submitForm(){
            if (this.student.id === undefined){
                this.createStudent();
            } else {
                this.editStudent();
            }
        },
        async getStudents(){
            Axios.get('https://franky88.pythonanywhere.com/students/?format=json', {
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Token ${access_token}`
                }
            })
            .then(response => {
                console.warn(response);
                return (this.studentlist=response)
            })
            .catch(error => console.log(error))
        },
        async createStudent(){
            await this.getStudents();
            Axios.post('https://franky88.pythonanywhere.com/students/?format=json', this.student, {
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Token ${access_token}`
                }
            })
            .then(response => {
                console.warn(response);
                // console.log(response);
            });
            await this.getStudents();
            this.student = {};
        },
        async editStudent() {
            await this.getStudents();
            Axios.put(`https://franky88.pythonanywhere.com/students/${this.student.id}/`, this.student, {
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Token ${access_token}`
                }
            })
            .then(response => {
                console.warn(response);
            });
            await this.getStudents();
            this.student = {};
        },
        async detailsStudent(student) {
            await this.getStudents();
            Axios.get(`https://franky88.pythonanywhere.com/students/${student.id}/`, {
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Token ${access_token}`
                }
            })
            .then(response => {
                console.warn(response);
            });
            await this.getStudents();
        },
        async deleteStudent(student) {
            await this.getStudents();
            Axios.delete(`https://franky88.pythonanywhere.com/students/${student.id}/`, {
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Token ${access_token}`
                }
            })
            .then(response => {
                console.warn(response);
            });
            await this.getStudents();
        },
        async clearList(){
          this.student = {};
        }
    }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
body {
  background-color: #D8E8E6;
}
</style>
