<template>
<div class="container">
    <div class="sidenav">
         <div class="signup-main-text">
            <h2> Регистрация</h2>
            <p>Создайте акаунт здесь.</p>
         </div>
      </div>
      <div class="main">
         <div class="col-md-6 col-sm-12">
            <div class="signup-form">
               <form class="form-signin" @submit.prevent="userRegister">
                  <div class="form-group">
                     <label>Имя пользователя</label>
                     <input id="inputUsername" class="form-control" placeholder="Имя пользователя"
                      required="" v-model="register.username"/>
                  </div>
                  <div class="form-group">
                     <label>Пароль</label>
                     <input type="password" id="inputPassword" class="form-control mt-2" placeholder="Пароль" required="" v-model="register.password">
                  </div>
                  <div class="form-group">
                     <label>Повторите пароль</label>
                     <input type="password" id="ReInputPassword" class="form-control mt-2" placeholder="Повторите пароль" required="" v-model="register.password2">
                  </div>
                  <button type="submit" class="btn btn-secondary">Создать акаунт</button>
               </form>
            </div>
         </div>
        <div class="toast-body text-danger">
                    {{ this.message }}
                  </div>
      </div>
    </div>
</template>

<script>

  export default {
    layout: "post_detail",
    data() {
      return {
        register: {
          username: '',
          password: '',
          password2: '',
        },
        message: '',
      }
    },
    methods: {
      async userRegister() {
        try {
          let response = await this.$axios.post('/api/register/', {
            username: this.register.username,
            password: this.register.password,
            password2: this.register.password2
          })
          console.log(response)
          await this.$auth.loginWith('local', {
            data: {
              username: this.register.username,
              password: this.register.password
            },
          })
          this.$router.back();
        }
          catch (err) {
          console.log(err)
          this.message = 'Что-то пошло не так, попробуйте еще раз!'
          }
      }
    },

  }
</script>

<style scoped>
</style>