<template>
    <button class="visib-button" @click="changeVisib">{{ buttonName }}</button>
</template>

<script>
export default {
  name: 'addingButton',
  data () {
    return {
      buttonName: 'ADD NEW COST+'
    }
  },
  methods: {
    changeVisib () {
      this.$emit('visib-state')
    }
  }
}
</script>

<style>
    .visib-button {
        background-color: rgb(35, 174, 130);
        transition: background 0.5s;
        border: none;
        color: white;
        font-weight: 500;
        line-height: 30px;
        font-size: 0.9em;
        cursor: pointer;
        padding: 0 20px 0 20px;
        margin-bottom: 15px;
    }
    .visib-button:hover {
        background-color: rgb(24, 118, 88);
    }
</style>
