<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Add Students</h4>
            </div>
            <div class="card-body">
                <!-- <ul class="alert alert-warning" v-if="Object.keys(this.errorList).length > 0">
                    <li class="mb-0 ms-3" v-for="(error, index) in this.errorList" :key="index">
                        {{error[0]}}
                    </li>
                </ul>
                <div class="mb-3">
                    <label for="">userID</label>
                    <input type="text" v-model="model.student.userId" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">title</label>
                    <input type="text" v-model="model.student.title" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">body</label>
                    <input type="text" v-model="model.student.body" class="form-control">
                </div> -->
                <div class="mb-3">
                    <label for="">Name</label>
                    <input type="text" v-model="model.student.name" class="form-control">
                </div>
                <div class="mb-3">
                    <button type="button" @click="saveStudent" class="btn btn-primary">Save</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'studentCreate',
    data(){
        return {
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
        this.getStudentData(this.$route.params.id)
    },
    methods: {
        saveStudent(){
            var mythis = this;
            //http://127.0.0.1:8000/add
            //https://jsonplaceholder.typicode.com/posts
            axios.post('http://127.0.0.1:8000/add/', this.model.student).then(res => {
                console.log(res.data)
                alert(res.data.message);
                this.model.student = {
                    // userId: '',
                    // title: '',
                    // body: ''
                    name: ''
                }
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