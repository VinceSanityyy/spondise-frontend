<script>
export default {
    data() {
        return {
            form:{
                email:'',
                password: ''
            },
            provider: 'google'
        }
    },
    created() {
        console.log('created')
    },
    methods:{
        login(){
            this.$axios.post('/login',{
                email: this.form.email,
                password: this.form.password
            }).then((res)=>{
                console.log(res.data)
                localStorage.setItem('auth_token',res.data.token)
                this.$router.push('/welcome')
            })
        },
        googleLogin(){
            window.location.href = `http://127.0.0.1:8000/api/login/${this.provider}`
            // this.$axios.get(`/login/${this.provider}`).then((res)=>{
            //     if(res.data.status == 200){
            //         this.$router.push('/welcome')
            //     } else {
            //         alert(1)
            //     }
            // })
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
                        <h5 class="card-title text-center mb-5 fw-light fs-5">Login to get started</h5>
                        <form @submit.prevent="login()">
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

                            <div class="form-check mb-3">
                                <a href="/register" class="form-check-label">
                                    Dont have an account?
                                </a>
                            </div>
                            <div class="d-grid">
                                <button class="btn btn-primary btn-login text-uppercase fw-bold" type="submit">Sign
                                    in</button>
                            </div>
                            <hr class="my-4">
                            <div class="d-grid mb-2">
                                <button class="btn btn-google btn-login text-uppercase fw-bold" type="button" @click="googleLogin()">
                                    <i class="fab fa-google me-2"></i> Sign in with Google
                                </button>
                            </div>
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