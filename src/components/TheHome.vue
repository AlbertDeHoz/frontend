<template>
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <form class="d-flex">
        <button class="btn btn-outline-success" type="button" @click="logOut()">LogOut</button>
      </form>
    </div>
    <div><p class="m-2"> {{ user.name }} </p></div>
    <div><p class="m-2"> {{ user.email }} </p></div>
    
  </div>
</nav>
</template>

<script>
export default {
    data(){
        return{
            user:{}
        }
    },
    methods:{
        logOut(){
            localStorage.removeItem('jwt');
            this.$router.push('/')
        },
        getUserDetails(){
            let user = localStorage.getItem('user');
           // let email = localStorage.getItem('email')
            let token = localStorage.getItem('jwt');
            if (token){
                this.user = JSON.parse(user);

            }
        }
    },
    created(){
        this.getUserDetails()
    }
}
</script>