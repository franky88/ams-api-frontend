<template>
<div id="app">
<div class="row">
    <div class="col-sm-4">
    <div class="card bg-light">
        <div class="card-header">
        Student Initial Details
        </div>
        <div class="card-body">
        <h3 class="card-title">Create Student Form</h3>
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
            <a class="btn text-sm-right" style="color: red;" @click="clearList">Clear</a>
        </form>
        </div>
    </div>
    </div>
    <div class="col-sm-8">
      <!-- Modal for delete -->
      <div class="modal fade" id="delete-student" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLongTitle">Student Details</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <div class="row">
                <div class="col-sm-4">
                  <div class="" style="background-color: teal; width:100%; height:100%; border-radius: 5%;">

                  </div>
                </div>
                <div class="col-sm-8">
                  <strong>{{ student.get_fullname }}</strong>
                  <br>
                  <small class="text-muted">Date Register: {{ student.date_register|formatDate }}</small>
                  <hr>
                  <button type="button" class="btn btn-outline-danger btn-sm" @click="deleteStudent(student)"><i class="fas fa-trash-alt"></i></button>
                </div>
              </div>

            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            </div>
          </div>
        </div>
      </div>
      <!-- Modal for details -->
      <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLongTitle">Student Details</h5>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <div class="row">
                <div class="col-sm-4">
                  <div class="" style="background-color: teal; width:100%; height:100%; border-radius: 5%;">

                  </div>
                </div>
                <div class="col-sm-8">
                  <strong>{{ student.get_fullname }}</strong>
                  <br>
                  <small class="text-muted">Date Register: {{ student.date_register|formatDate }}</small>
                  <hr>
                  <button type="button" class="btn btn-outline-danger btn-sm" @click="deleteStudent(student)"><i class="fas fa-trash-alt"></i></button>
                </div>
              </div>

            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            </div>
          </div>
        </div>
      </div>
    <div class="card">
        <div class="card-body">
        <h3 class="card-title">Student list</h3>
        <input class="form-control mr-sm-2" v-model="search" type="search" placeholder="Search Student" aria-label="Search">
        <br>
        <p class="text-muted">Filters</p>
        <hr>
        <table class="table table-sm table-hover">
            <thead>
            <tr>
                <th>Full Name</th>
                <th>Parent Contact</th>
                <th>Actions</th>
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
                <button type="button" class="btn btn-outline-info btn-sm" data-toggle="modal" data-target="#exampleModalCenter" :key="stud.id" @click="$data.student = stud">
  Details
</button>
                <!-- <button class="btn btn-outline-danger btn-sm mx-1" data-toggle="modal" data-target="#delete-student" :key="stud.id" @click="$data.student = stud"><i class="fas fa-trash-alt"></i></button> -->
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
