<template>
  <div class="container">
    <div class="sidenav-yelo">
         <div class="signin-main-text">
            <h2>Вход в акаунт</h2>
            <p>Войдите в аккаунт здесь.</p>
         </div>
      </div>
      <div class="main">
         <div class="col-md-6 col-sm-12">
            <div class="signin-form">
               <form class="form-signin" @submit.prevent="userLogin">
                  <div class="form-group">
                     <label>Имя пользователя</label>
                     <input id="inputUsername" class="form-control" placeholder="Имя пользователя" required="" v-model="login.username">
                  </div>
                  <div class="form-group">
                     <label>Пароль</label>
                     <input type="password" id="inputPassword" class="form-control mt-2" placeholder="Пароль" required="" v-model="login.password">
                  </div>
                  <button type="submit"  class="btn btn-secondary">Войти</button>
                  <div class="toast-body text-danger">
                    {{ this.message }}
                  </div>

               </form>
            </div>
         </div>
      </div>

    </div>
</template>

<script>

  export default {
    layout: "post_detail",
    data() {
      return {
        login: {
          username: '',
          password: ''
        },

        message: ''
      }
    },
    methods: {
      async userLogin() {
        try {
          let response = await this.$auth.loginWith('local', { data: this.login })
          console.log(response)
          this.$router.back();
        }
        catch (err) {
          console.log(err.message)
          this.message = 'Неправельный пароь или логин, попробуйте еще раз!'
        }
      }
    },

  }
</script>

<style scoped>
  
</style>