<template>
  <header class="header">
    <div class="header--container">
      <a class="header--logo">ZOZOTOWN</a>
      <form class="header--input">
        <label class="header--input__label">
          <img class="header--input__search" src="@/img/search.svg"/>
          <input class="header--input__box" placeholder="すべてのアイテムから探す"/>
        </label>
      </form>
      <div class="header--gnb">
        <a class="header--gnb__login">
          <div>ログイン</div>
        </a>
        <a class="header--gnb__item">
          <img class="header--gnb__img" src="@/img/bell.svg"/>
        </a>
        <a class="header--gnb__item">
          <img class="header--gnb__img" src="@/img/like.svg"/>
        </a>
        <a class="header--gnb__item">
          <img class="header--gnb__img" src="@/img/cart.svg"/>
        </a>
        <a class="header--gnb__item">
          <img class="header--gnb__img" src="@/img/hamburger.svg"/>
        </a>
      </div>
    </div>
  </header>
</template>

<script lang="ts" setup>
// Todo => 검색창을 선택할경우 포커스되며 배경이 투명하게 변함.
// Todo => 검색창에 검색어가 입력될 경우 오른쪽 끝에 X표시. X 표시를 누르면 검색어 리셋
</script>

<style lang="scss" scoped>
@import "@/assets/scss/components/header.scss";
</style>