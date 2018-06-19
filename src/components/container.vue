<template>
<div>
  <input type="number" v-model.number="inputNum">
  <div class="container" :style="containerStyle">
    <venn-chart :option='option' :data='data'></venn-chart>
  </div>
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
      containerStyle: {
        'border': '1px solid #ccc',
        'width': '500px',
        'margin': 'auto',
        'height': '300px'
      },
      data: {
        num: 123,
        percent: '20%'
      }
    }
  },
  computed: {
    option () {
      return {
        cy: this.inputNum,
        cx: 40,
        r: 40,
        'stroke-width': 1,
        fill: 'rgba(128, 211, 255, 0.5)',
        stroke: 'rgba(128, 211, 255, 1)'
      }
    }
  },
  watch: {
    // inputNum: (val) => {
    //   console.log(JSON.stringify(val))
    // }
  },
  mounted () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
  li {
    display: inline-block;
    margin: 0 10px;
  }
}
a {
  color: #42b983;
}
</style>
