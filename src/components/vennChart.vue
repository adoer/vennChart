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
      circleArr: [],
      circleOption: [
        {
          cy: 40,
          cx: 40,
          r: 40,
          'stroke-width': 1,
          fill: 'rgba(128, 211, 255, 0.5)',
          stroke: 'rgba(128, 211, 255, 1)'
        },
        {
          cy: 40,
          cx: 140,
          r: 40,
          'stroke-width': 1,
          fill: 'rgba(128, 211, 255, 0.5)',
          stroke: 'rgba(128, 211, 255, 1)'
        }
      ]
    }
  },
  props: {
    option: {
      type: Object,
      require: true
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
  computed: {
    venn () {
      return document.getElementById('venn-chart')
    }
  },
  methods: {
    setAttr () {
      this.circleArr.forEach((item, index) => {
        let curItem = Object.assign({}, this.circleOption[index], this.option.series[index].style)
        for (const [key, val] of Object.entries(curItem)) {
          item.setAttribute(key, val)
        }
      })
    },
    init () {
      this.vennH = this.venn.style.height = this.$el.parentNode.offsetHeight + 'px'
      this.vennW = this.venn.style.width = this.$el.parentNode.offsetWidth + 'px'
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
