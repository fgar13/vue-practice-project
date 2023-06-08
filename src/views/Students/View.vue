<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h4>
          Students
          <RouterLink to="/students/create" class="btn btn-primary float-end">
            Add Student
          </RouterLink>
        </h4>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead> 
            <tr>
              <th>ID</th>
              <th>Name</th>
              <th>Created</th>
            </tr>
          </thead>
          <tbody v-if="this.students.length>0">
            <tr v-for="(student, index) in students" :key="index">
              <td>{{ student.id }}</td>
              <td>{{ student.name }}</td>
              <td>{{ student.created }}</td>
              <td>
                <RouterLink :to="{path: '/students/'+student.id+'/edit'}" class="btn btn-success mx-2">
                  Edit
                </RouterLink>
                <button type="button" @click="deleteStudent(student.id)" class="btn btn-danger mx-2">
                  Delete
                </button>
              </td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr>
              <td colspan="7">Loading...</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'students',
  data() {
    return {
      students: [],
    };
  },
  mounted() {
    this.getStudents();
    console.log("I am here")
  },
  methods: {
    //https://jsonplaceholder.typicode.com/posts http://127.0.0.1:8000/
    getStudents() {
      axios.get('http://127.0.0.1:8000/').then((res) => {
        this.students = res.data//.students
        console.log(this.students)
      });
    },
    deleteStudent(studentId){
      console.log(studentId)
      if(confirm("U sure?")){
        axios.delete(`http://127.0.0.1:8000/delete/${studentId}/`).then(res => {
          alert("done")
        });
      }
    },
  },
};
</script>
