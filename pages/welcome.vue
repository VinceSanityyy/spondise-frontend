<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8">
                <div class="card border-primary">
                    <div class="card-header">
                        User Details
                    </div>
                    <div class="card-body">
                        <h5>Hi {{ this.name }}</h5>
                        <h5>Your email is {{ this.email }}</h5>
                        <h5>Your last login was on {{ this.last_login }}</h5>
                    </div>
                    <div class="card-footer">
                        <button @click="logout()" class="btn btn-primary" type="button">Logout</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    created() {
        this.getUserDetails()
    },
    data(){
        return{
            token: localStorage.getItem('auth_token'),
            name:'',
            email: '',
            last_login: ''
        }
    },
    methods:{
        getUserDetails(){
            this.$axios.get('/me',{
                headers:{
                    Authorization: `Bearer ${this.token}`
                }
            }).then((res)=>{
                console.log(res.data)
                this.name = res.data.data.name,
                this.email = res.data.data.email
                this.last_login = res.data.data.last_logged_in

            })
        },
        logout(){
            this.$axios.post('/logout',{
                headers:{
                    Authorization: `Bearer ${this.token}`
                }
            }).then((res)=>{
                if(res.data.status == 200){
                    this.$router.push('/login')
                }
            })
        }
    }
}
</script>