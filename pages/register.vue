<script>
export default {
    data(){
        return{
            form:{
                email:'',
                password:'',
                confirm_password:'',
                name:''
            }
        }
    },
    methods:{
        register(){
            this.$axios.post(`/register`,{
                email: this.form.email,
                password: this.form.password,
                confirm_password: this.form.confirm_password,
                name: this.form.name
            }).then((res)=>{
                console.log(res.data)
                if(res.data.status == 200){
                    localStorage.setItem('auth_token',res.data.token)
                    this.$router.push('/welcome')
                }
            })
        }
    }
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
                <div class="card border-0 shadow rounded-3 my-5">
                    <div class="card-body p-4 p-sm-5">
                        <h5 class="card-title text-center mb-5 fw-light fs-5">Register</h5>
                        <form @submit.prevent="register()">
                            <div class="form-floating mb-3">
                                <input type="text" v-model="form.name" class="form-control" 
                                    placeholder="">
                                <label for="floatingInput">Name</label>
                            </div>
                            <div class="form-floating mb-3">
                                <input type="email" v-model="form.email" class="form-control" id="floatingInput"
                                    placeholder="name@example.com">
                                <label for="floatingInput">Email address</label>
                            </div>
                            <div class="form-floating mb-3">
                                <input type="password" v-model="form.password" class="form-control" id="floatingPassword"
                                    placeholder="Password">
                                <label for="floatingPassword">Password</label>
                            </div>
                            <div class="form-floating mb-3">
                                <input type="password" v-model="form.confirm_password" class="form-control" id="floatingPassword"
                                    placeholder="Password">
                                <label for="floatingPassword">Confirm Password</label>
                            </div>
                            <div class="form-check mb-3">
                                <a href="/login" class="form-check-label">
                                    Already have an account?
                                </a>
                            </div>
                            <div class="d-grid">
                                <button class="btn btn-primary btn-login text-uppercase fw-bold" type="submit">Register</button>
                            </div>
                            <hr class="my-4">
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
body {
    background: #007bff;
    background: linear-gradient(to right, #0062E6, #33AEFF);
}

.btn-login {
    font-size: 0.9rem;
    letter-spacing: 0.05rem;
    padding: 0.75rem 1rem;
}

.btn-google {
    color: white !important;
    background-color: #ea4335;
}

.btn-facebook {
    color: white !important;
    background-color: #3b5998;
}
</style>
