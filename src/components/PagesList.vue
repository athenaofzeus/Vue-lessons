<template>
  <div class="pagesList">
    <span class="arrow arrow_left" @click="turnOnPage($event)">&lt;</span>
    <span class="num" v-for="n in pages" :key="n" @click="choosePage($event)">{{ n }}</span>
    <span class="arrow arrow_right" @click="turnOnPage($event)">&gt;</span>
  </div>
</template>

<script>
export default {
  name: 'pagesNums',
  props: {
    pages: {
      type: Number,
      default: 1
    },
    currentPage: {
      type: Number,
      default: 1
    }
  },
  methods: {
    choosePage (event) {
      this.$emit('picking-page', event.target.innerText)
    },
    turnOnPage (event) {
      this.$emit('pick-another', event.target.innerText)
    }
  }
}
</script>

<style>
    .pagesList {
        max-width: 300px;
        box-shadow: 0 0 2px 1px grey;
        padding: 5px 0 5px 0;
        position: relative;
        margin: 0 auto;
        margin-top: 15px;
    }
    .pagesList > span:hover {
        cursor: pointer;
        color: rgb(35, 174, 130);
    }
    .num {
        font-size: 0.7em;
        padding: 0 8px 0 8px;
    }
    .arrow_left {
        padding-right: 20px;
        position: absolute;
        left: 5px;

    }
    .arrow_right {
        padding-left: 20px;
        position: absolute;
        right: 5px;

    }
</style>
