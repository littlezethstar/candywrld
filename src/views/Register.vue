<template>
  <form @submit.prevent="register" class="form neu-border">
    <input
      class="form-input neu-border-inset"
      type="text"
      v-model="fullname"
      placeholder="Name"
      required
    />
    <input
      class="form-input neu-border-inset"
      type="email"
      v-model="email"
      placeholder="Email"
      required
    />
    <input
      class="form-input neu-border-inset"
      type="text"
      v-model="phone_number"
      placeholder="Contact"
      required
    />
    <input
      class="form-input neu-border-inset"
      type="password"
      v-model="password"
      placeholder="Password"
      required
    />
    <button type="submit" class="form-btn">Register</button>
    <!-- <div class="form-social-login">
      <button class="form-btn neu-border form-social-btn">
        <i class="fab fa-google"></i>
      </button>
      <button class="form-btn neu-border form-social-btn">
        <i class="fab fa-facebook-f"></i>
      </button>
    </div> -->

    <p>
      Already a member?
      <router-link :to="{ name: 'Login' }">Sign in</router-link>
    </p>
  </form>
</template>
<script>
export default {
  data() {
    return {
      fullname: "",
      email: "",
      phone_number: "",
      password: "",
    };
  },
  methods: {
    register() {
      fetch("https://pos-bkend.herokuapp.com/users", {
        method: "POST",
        body: JSON.stringify({
          fullname: this.fullname,
          email: this.email,
          phone_number: this.phone_number,
          password: this.password,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("User registered");
          localStorage.setItem("jwt", json.jwt);
          this.$router.push({ name: "Login" });
        })
        .catch((err) => {
          alert(err);
        });
    },
  },
};
</script>
<style>
.neu-border {
  border-radius: 30px;
  background: #f5f5f5;
  box-shadow: 8px 8px 15px #e4e4e4, -8px -8px 15px #ffffff;
}
.neu-border-inset {
  border-radius: 30px;
  background: #f5f5f5;
  box-shadow: inset 8px 8px 15px #e4e4e4, inset -8px -8px 15px #ffffff;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 40px;
  gap: 20px;
  width: 100%;
  max-width: 600px;
  margin-inline: auto;
}

.form-heading {
  text-align: center;
  text-transform: uppercase;
}

.form-input,
.form-btn {
  border: none;
  outline: none;
  padding: 20px;
}

.form-btn {
  cursor: pointer;
  transition: all 0.1s linear;
}

.form-btn:hover {
  transform: scale(1.05);
}

.form-social-login {
  display: flex;
  justify-content: space-between;
}

.form-social-btn {
  width: 45%;
  color: #333;
}
</style>
