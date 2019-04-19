<template>
    <div id="app">
      <h1>Dinner calculator</h1>
      <Table
        :dinner=100
        :tip=9
        :people=2
      ></Table>
    </div>
</template>

<script>
import Table from './components/Table.vue'

export default {
  name: 'app',
  components: {
    Table
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
