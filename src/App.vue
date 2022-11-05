<template>
  <div id="app">
    <header>
      <div>My personal costs</div>
    </header>
    <main>
      <addingButton @visib-state="ChangeVisib"/>
      <payForm :visibility="visibility" @new-payment="addNewPayment"/>
      <payDisplay :items="paymentsList" :currentPage="currentPage" />
      <pagesNums :pages="countPages" @picking-page="changePage" :currentPage="currentPage" @pick-another="pickAnotherPage" />
    </main>
  </div>
</template>

<script>
import addingButton from './components/ButtonAdding.vue'
import payDisplay from './components/PaymentsDisplay.vue'
import payForm from './components/AddPaymentForm.vue'
import pagesNums from './components/PagesList.vue'

export default {
  name: 'App',
  components: {
    addingButton,
    payDisplay,
    payForm,
    pagesNums
  },
  data () {
    return {
      paymentsList: [],
      visibility: false,
      currentPage: 1
    }
  },
  methods: {
    fetchData () {
      return [
        {
          id: 1,
          date: '28.03.2020',
          category: 'Food',
          value: 169
        },
        {
          id: 2,
          date: '24.03.2020',
          category: 'Transport',
          value: 360
        },
        {
          id: 3,
          date: '24.03.2020',
          category: 'Food',
          value: 532
        }
      ]
    },
    addNewPayment (data) {
      const id = this.paymentsList.length + 1
      this.paymentsList.push({ id: id, ...data })
    },
    ChangeVisib () {
      this.visibility = !this.visibility
    },
    changePage (target) {
      this.currentPage = Number(target)
    },
    pickAnotherPage (target) {
      if (target === '<' && this.currentPage > 1) {
        this.currentPage -= 1
      } else if (target === '>' && this.currentPage < this.countPages) {
        this.currentPage += 1
      }
    }
  },
  computed: {
    countPages () {
      return Math.ceil(this.paymentsList.length / 5)
    }
  },
  created () {
    setTimeout(() => {
      this.paymentsList = this.fetchData()
    }, 1000)
  }
}
</script>

<style>
#app {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  max-width: 1000px;
  text-align: center;
  margin: 0 auto;
  padding: 0;
  padding-top: 30px;
}
header {
  font-weight: 800;
  font-size: 2em;
  margin-bottom: 20px;
}
</style>
