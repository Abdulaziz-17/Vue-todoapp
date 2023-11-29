<template>
  <nav class="nav">
    <Transition name="item">
      <div class="nav__item" v-show="nav">
        <button class="nav__lang"  @click="changeLang">{{lang}}</button>
        <h1 class="nav__title">{{$t("appbartitle")}}</h1>
        <button class="nav__search" @click="nav = !nav">
          <img src="@/assets/images/search.svg" alt="" />
        </button>
      </div>
    </Transition>
    <Transition name="form">
      <div class="nav__form" v-show="!nav">
        <button class="nav__back" @click="(nav = !nav), clear()">
          <img src="@/assets/images/back.svg" alt="" />
        </button>
        <input
          v-model="search"
          type="text"
          :placeholder="$t('appbarseacrch')"
          class="nav__input"
        />
        <button class="nav__close" @click="clear">
          <img src="@/assets/images/close.svg" alt="" />
        </button>
      </div>
    </Transition>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      nav: true,
      search: "",
    };
  },
  methods: {
    clear() {
      this.search = "";
    },
   changeLang(){
    let lang = this.lang == 'ru' ? 'uz' : 'ru'
    this.$emit('changeLang', lang)
    this.$i18n.locale = lang
   }
  },
  watch: {
    search(value) {
      this.$emit('search', value)
    }
  },
  props: {
    lang: String,
  },
};
</script>

<style lang="scss" scoped>
</style>