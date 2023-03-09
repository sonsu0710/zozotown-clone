<template>
  <header class="header">
    <div class="header--container">
      <a class="header--logo">ZOZOTOWN</a>
      <div class="header--input">
        <form>
          <label
              class="header--input__label"
              :class="inputValue ? borderBottomRadius : ''"
          >
            <img class="header--input__search" src="@/img/search.svg" alt="search"/>
            <input
                class="header--input__box"
                autocomplete="off"
                placeholder="すべてのアイテムから探す"
                name="header-search"
                @input="inputValue = $event.target.value"
            />
          </label>
          <div v-if="inputValue" class="header--search-box">
            <div
                class="header--search-box__result"
                v-for="(item, idx) in resultValue"
                :key="item.value"
                :class="(idx === 9 ? searchModalLast : '') || (idx === 0 ? searchModalFirst : '')"
            >
              {{item.value}}
            </div>
          </div>
        </form>
      </div>
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
import {computed, ref, watch} from "vue";
import axios from "axios";

// todo => 검색창을 선택할경우 포커스되며 배경이 투명하게 변함.


// todo => 검색창에 검색어가 입력될 경우 오른쪽 끝에 X표시. X 표시를 누르면 검색어 리셋


// todo => 검색어 입력시 예상 검색어 모달창 나오도록 표시
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

const borderBottomRadius = computed(() => {
  return "header--input__label-bottom"
})

const searchModalFirst = computed(() => {
  return "header--search-box__result-first";
})
const searchModalLast = computed(() => {
  return "header--search-box__result-last";
})

// todo 검색창에서 자동완성되는 경우 해당 인풋 백그라운드 색상 제거

</script>

<style lang="scss" scoped>
@import "@/assets/scss/components/header.scss";
</style>