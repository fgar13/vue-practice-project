<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h4>
          Students
          <RouterLink to="/student/create" class="btn btn-primary float-end">
            Add Student
          </RouterLink>
        </h4>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead> 
            <tr>
              <th>UserID</th>
              <th>ID</th>
              <th>Title</th>
              <th>Body</th>
            </tr>
          </thead>
          <tbody v-if="this.students.length>0">
            <tr v-for="(student, index) in students" :key="index">
              <td>{{ student.userId }}</td>
              <td>{{ student.id }}</td>
              <td>{{ student.title }}</td>
              <td>{{ student.body }}</td>
              <td>
                <RouterLink :to="{path: '/students/'+student.id+'/edit'}" class="btn btn-success mx-2">
                  Edit
                </RouterLink>
                <button type="button" class="btn btn-danger mx-2">
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
      axios.get('https://jsonplaceholder.typicode.com/posts').then((res) => {
        this.students = res.data//.students
        console.log(this.students)
      });
    },
  },
};
</script>
