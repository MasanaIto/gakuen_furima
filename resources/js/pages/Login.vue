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
                <label for="login-email">メールアドレス</label>
                <input type="text" class="form__item" id="login-email" v-model="loginForm.email">
                <label for="login-password">パスワード</label>
                <input type="password" class="form__item" id="login-password" v-model="loginForm.password">
                <div class="form__button">
                    <button type="submit" class="button button--inverse">ログインする</button>
                </div>
            </form>
        </div>
    </div>
    <div class="panel" v-show="tab === 2">Register Form</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tab: 1,
      loginForm: {
          email: '',
          password: ''
      }
    }
  },
  methods: {
      login () {
          console.log(this.loginForm)
      }
  }
}
</script>
