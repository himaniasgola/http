<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Http</h1>
                <div class="form-group">
                    <label>Username</label>
                        <input class="form-control" type="text" v-model="user.username">
                </div>
                <div class="form-group">
                    <label>Mail</label>
                        <input class="form-control" type="text" v-model="user.email">
                </div>
                <button @click="submit">submit</button>
                <hr>
                <button @click="fetchData">Get data</button>
                <br><br>
                <li v-for="u in users" :key="u">{{u.username }} - {{ u.email }}</li>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                user: {
                    username: '',
                    email: ''
                },
                users: [],
                resource: {}
            }
        },
        methods: {
            submit() {
//                   this.$http.post('data.json',this.user)
//              .then(response => {
//                  console.log(response)
//                },
 //               error => {
//                    console.log(error)
//                });
        this.resource.save({},this.user);
            },
            fetchData() {
                this.$http.get('data.json')
                .then(response => {
                    return response.json();
                })
                .then(data => {
                    const resultArray = [];
                    for(let key in data) {
                        resultArray.push(data[key]);
                    }
                    this.users = resultArray;
                });
            }
        },
        created() {
            this.resource = this.$resource('data.json');
        }
    }
</script>

<style>
</style>
