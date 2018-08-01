<template>
    <svg xmlns="http://www.w3.org/2000/svg" id="venn-chart" version="1.1"></svg>
</template>

<script>
export default {
  name: 'vennChart',
  data () {
    return {
      c1: null,
      c2: null,
      t1: null
    }
  },
  props: {
    option: {
      type: Object,
      require: true
    }
  },
  computed: {
    venn () {
      return document.getElementById('venn-chart')
    }
  },
  watch: {
    option: {
      handler: function (val) {
        this.setAttr()
      },
      deep: true
    }
  },
  methods: {
    refresh () {
      setTimeout(() => {
        this.setAttr()
      }, 200)
    },
    vennH () {
      return this.$el.parentNode.offsetHeight
    },
    vennW () {
      return this.$el.parentNode.offsetWidth
    },
    intersectionOption () {
      return {
        // x: '50%',
        x: this.vennW() / 2,
        y: this.vennH() / 2,
        style: {
          'fill': 'red',
          'font-size': '24px',
          'font-weight': 'bold',
          'text-anchor': 'middle',
          'dominant-baseline': 'middle'
        }
      }
    },
    circleOption () {
      let cR = this.vennH() / 2
      let offset = 80
      return [
        {
          cy: this.vennH() / 2,
          // cx: this.vennW() / 2 - offset,
          cx: this.vennW() / 2 - offset,
          r: cR,
          'stroke-width': 1,
          fill: 'rgba(128, 211, 255, 0.5)',
          stroke: 'rgba(128, 211, 255, 1)'
        },
        {
          cy: this.vennH() / 2,
          cx: this.vennW() / 2 + offset,
          r: cR,
          'stroke-width': 1,
          fill: 'rgba(128, 211, 255, 0.5)',
          stroke: 'rgba(128, 211, 255, 1)'
        }
      ]
    },
    setAttr () {
      this.venn.style.height = this.vennH() + 'px'
      this.venn.style.width = this.vennW() + 'px'
      if (!(this.c1 && this.c2 && this.t1)) {
        // 圆
        this.c1 = document.createElementNS('http://www.w3.org/2000/svg', 'circle')
        this.c2 = document.createElementNS('http://www.w3.org/2000/svg', 'circle')
        // 文本
        this.t1 = document.createElementNS('http://www.w3.org/2000/svg', 'text')
        // this.circleArr = [c1, c2, t1]
      }
      [this.c1, this.c2].forEach((item, index) => {
        let curItem = Object.assign({}, this.circleOption()[index], this.option.series[index].styleObj)
        for (const [key, val] of Object.entries(curItem)) {
          item.setAttribute(key, val)
        }
      })
      this.t1.innerHTML = this.option.intersection.val
      let curIntersectionOption = this.intersectionOption()
      curIntersectionOption.style = Object.assign({}, this.intersectionOption().style, this.option.intersection.style)
      console.log(curIntersectionOption)
      for (const [key, val] of Object.entries(curIntersectionOption)) {
        if (key === 'style') {
          let curStyleStr = ''
          for (const [k, v] of Object.entries(val)) {
            curStyleStr += k + ':' + v + ';'
          }
          this.t1.setAttribute(key, curStyleStr)
        } else {
          this.t1.setAttribute(key, val)
        }
      }
    },
    init () {
      this.setAttr()
      let svgElArr = [this.c1, this.c2, this.t1]
      svgElArr.forEach(el => {
        this.venn.appendChild(el)
      })
    }
  },
  mounted () {
    this.init()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
