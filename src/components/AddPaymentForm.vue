<template>
  <div class="inputsBox" v-show="visibility">
    <input placeholder="Date" v-model="date">
    <input placeholder="Category" v-model="category">
    <input placeholder="Value" v-model="value">
    <button @click="addNewPayment" class="addButton">Add +</button>
  </div>
</template>

<script>
export default {
  name: 'payForm',
  data () {
    return {
      date: '',
      category: '',
      value: ''
    }
  },
  props: {
    visibility: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    addNewPayment () {
      const { value, category, date, getCurrentDate } = this
      const data = {
        date: date || getCurrentDate,
        category,
        value
      }
      this.$emit('new-payment', data)
    }
  },
  computed: {
    getCurrentDate () {
      const today = new Date()
      const d = today.getDate()
      const m = today.getMonth() + 1
      const y = today.getFullYear()
      return `${d}.${m}.${y}`
    }
  }
}
</script>

<style>
    .inputsBox {
        height: 180px;
        max-width: 300px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: end;
        margin: 0 auto;
    }
    input {
        height: 25px;
        width: calc(100% - 8px);
    }
    .addButton {
        background-color: rgb(35, 174, 130);
        transition: background 0.5s;
        border: none;
        color: white;
        font-weight: 700;
        line-height: 30px;
        font-size: 1em;
        word-spacing: 2em;
        cursor: pointer;
        width: 45%;
    }
    .addButton:hover {
        background-color: rgb(24, 118, 88);
    }
</style>
