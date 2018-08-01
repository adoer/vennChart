<template>
<div>
  <div style="margin-bottom:10px">
    <span>Width:</span> <input type="number" v-model.number="inputW">
    <span>Height:</span> <input type="number" v-model.number="inputH">
  </div>
  <div class="container" :style="containerStyle">
    <venn-chart ref='venn' :option='option'></venn-chart>
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
      inputW: 500,
      inputH: 300,
      option: {
        // style: {
        //   'stroke-width': 1,
        //   'fill': 'rgba(128, 211, 255, 0.5)',
        //   'stroke': 'rgba(128, 211, 255, 1)'
        // },
        // 第一个韦恩图值 第二个韦恩图值 公共值
        intersection: {
          val: 1666,
          style: {
            'fill': 'blue',
            'font-size': '24px',
            'font-weight': 'bold'
          }
        },
        series: [
          {
            val: 123,
            styleObj: {
              fill: 'rgba(128, 211, 255, 0.5)',
              stroke: 'rgba(128, 211, 255, 1)'
            }
          },
          {
            val: 123,
            styleObj: {
              fill: 'rgba(225, 117, 159, 0.5)',
              stroke: 'rgba(225, 117, 159, 1)'
            }
          }
        ]
      }
    }
  },
  computed: {
    containerStyle () {
      return {
        'width': this.inputW + 'px',
        'height': this.inputH + 'px',
        'margin': 'auto',
        'background': '#f8f8f8'
      }
    }
  },
  watch: {
    inputH: function (val) {
      this.$refs.venn.refresh()
    }
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
