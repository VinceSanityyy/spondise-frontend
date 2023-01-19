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
            name:'',
            email: '',
            last_login: ''
        }
    },
    methods:{
        getUserDetails(){
            const url = new URL(window.location.href);
            let user = url.searchParams.get('user')
            if(!user){
                this.$axios.get('/me',{
                headers:{
                    Authorization: `Bearer ${localStorage.getItem('auth_token')}`
                }
            }).then((res)=>{
                console.log(res.data)
                this.name = res.data.data.name,
                this.email = res.data.data.email
                this.last_login = res.data.data.last_logged_in
            })
            }else{
                localStorage.setItem('auth_token',url.searchParams.get('token'))
                this.$axios.get('/me',{
                headers:{
                    Authorization: `Bearer ${url.searchParams.get('token')}`
                }
            }).then((res)=>{
                console.log(res.data)
                this.name = res.data.data.name,
                this.email = res.data.data.email
                this.last_login = res.data.data.last_logged_in
            })
            }
       
        },
        logout(){
            this.$axios.post('/logout',{
            },{
                headers:{
                    Authorization: `Bearer ${localStorage.getItem('auth_token')}`,
                }
            }).then((res)=>{
                if(res.data.status == 200){
                    localStorage.clear()
                    this.$router.push('/login')
                }
            })
        }
    }
}
</script>

<style scoped>
.card {
  position: absolute;
  margin: auto;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  width: 800px;
  height: 200px;
}
</style>