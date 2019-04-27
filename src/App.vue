<template>
    <div id="app">
      <h1>Dinner calculator</h1>
      <DinnerTable/>
    </div>
</template>

<script>
import DinnerTable from './components/DinnerTable.vue'

export default {
  name: 'app',
  components: {
    DinnerTable
  }
}
</script>

<style lang="scss">
#app {
        color: #999;
        font-family: 'Arial';

        h1 {
            text-align: center;
            margin-top: 40px
        }
        
}
</style>
