<template>
  <div>

    <container>
      <form>

        <v-text-field
          v-model="username"
          label="Username"
          required
        ></v-text-field>
        <v-text-field
          v-model="password"
          label="Password"
          required
        ></v-text-field>

        <v-btn
          class="mr-4"
          @click="submit"
        >login</v-btn>
        <v-btn @click="register">register</v-btn>
      </form>
    </container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      username: "",
      password: ""
    };
  },
  methods: {
    submit: function() {
      let instance = this;
      this.axios
        .post("users/login", {
          username: this.username,
          password: this.password
        })
        .then(response => {
          console.log(response);
          if(response.status == 200){
            localStorage.setItem('token',response.data.token);
            localStorage.setItem('user',response.data.data.username);
            localStorage.setItem('_id',response.data.data._id);
            instance.$router.push('/');
          }
        })
        .catch(err => {
          console.log(err);
        });
    },
    register: function() {
      this.$router.push('/register')
    }
  }
};
</script>
