<template>
  <div class="container--small">
    <ul class="tab">
      <li
        class="tab__item"
        :class="{'tab__item--active': tab === 1 }"
        @click="tab = 1"
      >ログイン</li>
      <li
        class="tab__item"
        :class="{'tab__item--active': tab === 2 }"
        @click="tab = 2"
      >新規登録</li>
    </ul>
    <div class="panel" v-show="tab === 1">
        <div class="panel" v-show="tab === 1">
            <form class="form" @submit.prevent="login">
                <div v-if="loginErrors" class="errors">
                    <ul v-if="loginErrors.email">
                        <li v-for="msg in loginErrors.email" :key="msg">{{ msg }}</li>
                    </ul>
                </div>
                <label for="login-email">メールアドレス</label>
                <input type="text" class="form__item" id="login-email" v-model="loginForm.email">
                <div v-if="loginErrors" class="errors">
                    <ul v-if="loginErrors.password">
                        <li v-for="msg in loginErrors.password" :key="msg">{{ msg }}</li>
                    </ul>
                </div>
                <label for="login-password">パスワード</label>
                <input type="password" class="form__item" id="login-password" v-model="loginForm.password">
                <div class="form__button">
                    <button type="submit" class="button button--inverse">ログインする</button>
                </div>
            </form>
        </div>
    </div>
    <div class="panel" v-show="tab === 2">
        <form class="form" @submit.prevent="register">
            <label for="username">ユーザー名</label>
            <input type="text" class="form__item" id="username" v-model="registerForm.name">
            <label for="email">メールアドレス</label>
            <input type="text" class="form__item" id="email" v-model="registerForm.email">
            <label for="password">パスワード</label>
            <input type="password" class="form__item" id="password" v-model="registerForm.password">
            <label for="password-confirmation">パスワード（再入力）</label>
            <input type="password" class="form__item" id="password-confirmation" v-model="registerForm.password_confirmation">
            <div class="form__button">
                <button type="submit" class="button button--inverse">登録</button>
            </div>
        </form>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {
      tab: 1,
      loginForm: {
          email: '',
          password: ''
      },
      registerForm: {
          name: '',
          email: '',
          password: '',
          password_confirmation: ''
      }
    }
  },
  methods: {
      async login () {
          // authストアのloginアクションを呼び出す
          await this.$store.dispatch('auth/login', this.loginForm)

          if (this.apiStatus) {
              // トップページに移動する
              this.$router.push('/')
          }
      },
      async register () {
          // authストアのregisterアクションを呼び出す
          await this.$store.dispatch('auth/register', this.registerForm)

          // トップページに戻る
          this.$router.push('/')
      },
      clearError () {
          this.$store.commit('auth/setLoginErrorMessages', null)
      }
  },
  created () {
      this.clearError()
  },
  computed: {
    ...mapState({
        apiStatus: state => state.auth.apiStatus,
        loginErrors: state => state.auth.loginErrorMessages
    })
  }
}
</script>
