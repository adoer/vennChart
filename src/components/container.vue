<template>
  <div class="container">
    <input type="number" v-model.number="inputNum">
    <venn-chart :option='option' :data='data'></venn-chart>
  </div>
</template>

<script>
import vennChart from './vennChart'
export default {
  name: 'container',
  components: {
    vennChart
  },
  data () {
    return {
      inputNum: 100,
      data: {
        num: 123,
        percent: '20%'
      }
    }
  },
  computed: {
    option () {
      return {
        width: this.inputNum,
        height: 30,
        style: 'fill:rgb(0,0,255);stroke-width:1;stroke:rgb(0,0,0)'
      }
    }
  },
  watch: {
    // inputNum: (val) => {
    //   console.log(JSON.stringify(val))
    // }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
