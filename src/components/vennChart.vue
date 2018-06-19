<template>
  <div>
    <svg xmlns="http://www.w3.org/2000/svg" id="venn-chart" version="1.1"></svg>
  </div>
</template>

<script>
export default {
  name: 'vennChart',
  data () {
    return {
      circleArr: []
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
    },
    vennH () {
      return this.$el.parentNode.offsetHeight
    },
    vennW () {
      return this.$el.parentNode.offsetWidth
    },
    circleOption () {
      let cR = this.vennH / 2
      let offset = 80
      return [
        {
          cy: this.vennH / 2,
          cx: this.vennW / 2 - offset,
          r: cR,
          'stroke-width': 1,
          fill: 'rgba(128, 211, 255, 0.5)',
          stroke: 'rgba(128, 211, 255, 1)'
        },
        {
          cy: this.vennH / 2,
          cx: this.vennW / 2 + offset,
          r: cR,
          'stroke-width': 1,
          fill: 'rgba(128, 211, 255, 0.5)',
          stroke: 'rgba(128, 211, 255, 1)'
        }
      ]
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
      this.setAttr()
    },
    setAttr () {
      this.circleArr.forEach((item, index) => {
        let curItem = Object.assign({}, this.circleOption[index], this.option.series[index].style)
        for (const [key, val] of Object.entries(curItem)) {
          item.setAttribute(key, val)
        }
      })
    },
    init () {
      this.venn.style.height = this.vennH + 'px'
      this.venn.style.width = this.vennW + 'px'
      const c1 = document.createElementNS('http://www.w3.org/2000/svg', 'circle')
      const c2 = document.createElementNS('http://www.w3.org/2000/svg', 'circle')
      this.circleArr = [c1, c2]
      this.setAttr()
      this.venn.appendChild(c1)
      this.venn.appendChild(c2)
      // this.circleArr.forEach(el => {
      //   el = document.createElementNS('http://www.w3.org/2000/svg', 'circle')
      //   this.venn.appendChild(el)
      // })
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
