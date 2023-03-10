<template>
  <header class="header">
    <div class="header--container">
      <h1 class="header--logo">
        <a class="header--logo__href" aria-label="ZOZOTOWN">
          <img src="@/assets/img/logo.svg" alt="logo" class="svg--logo"/>
        </a>
      </h1>
      <div class="header--search-box">
        <div :class="openBgOpacity ? addOverlay : removeOverlay"/>
        <div class="relative-w100" :class="[openBgOpacity ? toZindexModel : '']">
          <form class="relative-w100">
            <label class="align-center">
              <div class="search-icon--wrapper">
                <img
                    src="@/assets/img/search.svg"
                    alt="search"
                    class="svg--search"
                />
              </div>
              <input
                  type="search"
                  class="header--search-box__input"
                  :class="(resultValue.length !== 0) ? borderBottomRadius : ''"
                  autocomplete="off"
                  placeholder="すべてのアイテムから探す"
                  name="header-search"
                  @input="inputValue = $event.target.value"
                  @focus="openBgOpacity = true"
                  ref="inputTag"
              />
              <button
                  type="reset"
                  v-if="inputValue !== ''"
                  class="header--search-box__reset-btn"
                  :class="openBgOpacity ? toZindexModel : ''"
                  @click="resultValue = []; inputValue = ''; $refs.inputTag.value = '';"
                  name="input-reset"
              >
                <img
                    src="@/assets/img/reset.svg"
                    alt="reset"
                    class="svg--reset"
                    aria-label="入力テキストを削除する"
                />
              </button>
            </label>
          </form>
          <div
              class="search-result-box"
              :class="resultValue.length !== 0 ? addBorderBottom : ''"
          >
            <div
                class="search-result-box--box-padding"
                v-for="item in resultValue"
                :key="item.value"
            >{{ item.value }}
            </div>
          </div>
        </div>
      </div>
      <div class="gnb">
        <div class="gnb--login-box">
          <a>ログイン</a>
        </div>
        <div class="gnb--item-box">
          <a><img src="@/assets/img/bell.svg"/></a>
        </div>
        <div class="gnb--item-box">
          <a><img src="@/assets/img/like.svg"/></a>
        </div>
        <div class="gnb--item-box">
          <a><img src="@/assets/img/cart.svg"/></a>
        </div>
        <div class="gnb--item-box">
          <a><img src="@/assets/img/hamburger.svg"/></a>
        </div>
      </div>
    </div>
  </header>
</template>

<script lang="ts" setup>
import {computed, onMounted, ref, watch, watchEffect} from "vue";
import axios from "axios";
import {$ref} from "vue/macros";

const inputValue = ref("");
const resultValue = ref([]);

const getSearchData = async () => {
  await axios
      .get(`https://completion.amazon.com/api/2017/suggestions?session-id=133-4736477-7395454&customer-id=&request-id=4YM3EXKRH1QJB16MSJGT&page-type=Gateway&lop=en_US&site-variant=desktop&client-info=amazon-search-ui&mid=ATVPDKIKX0DER&alias=aps&b2b=0&fresh=0&ks=71&prefix=${inputValue.value}&event=onKeyPress&limit=11&fb=1&suggestion-type=KEYWORD`)
      .then((res) => {
        resultValue.value = res.data.suggestions;
      })
};
watch(inputValue, () => {
  getSearchData();
})

// class control
const borderBottomRadius = computed(() => {
  return "border-bottom-radius-change"
})

const addBorderBottom = computed(() => {
  return 'add-border-bottom'
})

const addOverlay = computed(() => {
  return 'overlay'
})

const removeOverlay = computed(() => {
  return ''
})

const toZindexModel = computed(() => {
  return 'z-index-model'
})

// switch btn
const openBgOpacity = ref(false);


// todo 검색창에서 자동완성되는 경우 해당 인풋 백그라운드 색상 제거

</script>

<style lang="scss" scoped>
@import "@/assets/scss/components/layout/_header.scss";
</style>