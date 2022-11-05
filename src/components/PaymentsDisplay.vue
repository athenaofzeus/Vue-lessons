<template>
  <table cellspacing="0">
    <thead>
      <tr>
        <th>#</th>
        <th>Date</th>
        <th>Category</th>
        <th>Value</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(dict, idx) in items.slice(5 * currentPage - 5, 5 * currentPage)" :key="idx">
        <td v-for="(val, keys) in dict" :key="keys">{{ val }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'payDisplay',
  props: {
    items: {
      type: Array,
      default () {
        return []
      }
    },
    currentPage: {
      type: Number,
      default: 1
    }
  }
}
</script>

<style>
  table {
    margin: 0 auto;
    padding-top: 20px
  }
  td {
    border-bottom: 1px solid black;
  }
  th, td {
    font-size: 0.8em;
    padding: 5px 30px 5px 30px;
  }
</style>
