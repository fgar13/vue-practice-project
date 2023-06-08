<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Edit Students</h4>
            </div>
            <div class="card-body">
                <div class="mb-3">
                    <label for="">Name</label>
                    <input type="text" v-model="model.student.name" class="form-control">
                </div>
                <div class="mb-3">
                    <button type="button" @click="updateStudent" class="btn btn-primary">Update</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'studentEdit',
    data(){
        return {
            studentId: '',
            errorList: '',
            model: {
                student: {
                    // userId: '',
                    // title: '',
                    // body: ''
                    name: ''
                }
            }
        }
    },
    mounted(){
        console.log(this.$route.params.id);
        this.studentId = this.$route.params.id;
        this.getStudentData(this.$route.params.id)
    },
    methods: {
        getStudentData(studentId){
            axios.get(`http://127.0.0.1:8000/edit/${studentId}/`).then(res => {
                console.log(res.data)
                alert("alert")
                this.model.student.name = res.data.student.name
            })
            .catch(function (error) {
                if (error.response) {
                    if(error.response.status == 404){
                        mythis.errorList = error.response//.data;
                    }
                console.log(error.response.data);
                console.log(error.response.status);
                console.log(error.response.headers);
                } else if (error.request) {
                console.log(error.request);
                } else {
                console.log('Error', error.message);
                }
            });
         },
        updateStudent(){
            var mythis = this;
            //http://127.0.0.1:8000/add
            //https://jsonplaceholder.typicode.com/posts
            axios.put(`http://127.0.0.1:8000/edit/${this.studentId}/`, this.model.student).then(res => {
                console.log(res.data)
                alert(res.data.message);
                // this.model.student = {
                //     // userId: '',
                //     // title: '',
                //     // body: ''
                //     name: ''
                // }
            })
            .catch(function (error) {
                if (error.response) {
                    if(error.response.status == 422){
                        mythis.errorList = error.response//.data;
                    }

                    // if(error.response.status != 200){
                    //     mythis.errorList = error.response.data.errors;
                    // }
                console.log(error.response.data);
                console.log(error.response.status);
                console.log(error.response.headers);
                } else if (error.request) {
                console.log(error.request);
                } else {
                console.log('Error', error.message);
                }
                // console.log(error.config);
            });
        }
    },
}
</script>