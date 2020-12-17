<template>
  <div class="container row">
    <form class="col-4 offset-md-4">
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">Email address</label>
        <input
          type="email"
          class="form-control"
          id="exampleInputEmail1"
          aria-describedby="emailHelp"
          v-model="login.email"
        />
        <div id="emailHelp" class="form-text">
          We'll never share your email with anyone else.
        </div>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">Password</label>
        <input
          type="password"
          class="form-control"
          id="exampleInputPassword1"
          v-model="login.password"
        />
      </div>
      <button type="submit" class="btn btn-primary" @click.prevent="loginUser">
        Submit
      </button>
    <!--  <pre>
    {{ login }}
  </pre>-->
    </form>
  </div>
</template>



<script>
import swal from "sweetalert";

export default {
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async loginUser() {
      //console.log(this.login)

      try {
        //let response = await this.$http.post("/api/auth/signin", this.login);
        let response = await this.$http.post("/api/user/signin", this.login);
        // swal("Exito", "Login Correcto", "success");
        console.log(response.data.usuario[0].name);
        let token = response.data.accessToken;
        let user = response.data.usuario[0];
        // console.log(user)
        localStorage.setItem("jwt", token);
        localStorage.setItem("user", JSON.stringify(user));
        //localStorage.setItem("email", JSON.stringify(user[0].email));

        if (token) {
          this.$router.push("/home");
          swal("Exito", "Login Correcto", "success");
        }
      } catch (error) {
        let errorMostrar = "Algo salió mal";
        if (error["message"] == "Request failed with status code 404") {
          errorMostrar = "Error de usuario";
        }
        if (error["message"] == "Request failed with status code 401") {
          errorMostrar = "Usuario o clave incorrecta";
        }
        swal("UPS", errorMostrar, "error");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
