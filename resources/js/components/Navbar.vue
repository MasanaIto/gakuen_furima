<template>
  <nav class="navbar">
    <RouterLink class="navbar__brand" to="/">
      ガクエンフリマ
    </RouterLink>
    <div class="navbar__menu">
      <div class="navbar__item">
        <button class="button">
          <i class="icon ion-md-add"></i>
          出品する！
        </button>
      </div>
      <span class="navbar__item">
        ユーザー名
      </span>
      <div class="navbar__item">
        <RouterLink class="button button--link" to="/login">
          ログイン / 新規登録
        </RouterLink>
      </div>
    </div>
  </nav>
</template>
