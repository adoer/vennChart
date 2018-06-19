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
    }
  },
  props: {
    data: {
      type: Object,
      required: true
    },
    option: {
      type: Object,
      default () {
        return {
          width: 100,
          height: 30,
          style: 'fill:rgb(0,0,255);stroke-width:1;stroke:rgb(0,0,0)'
        }
      }
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
      for (const [key, val] of Object.entries(this.option)) {
        this.rect.setAttribute(key, val)
      }
    },
    init () {
      this.venn.style.height = this.$el.parentNode.offsetHeight + 'px'
      this.venn.style.width = this.$el.parentNode.offsetWidth + 'px'
      this.rect = document.createElementNS('http://www.w3.org/2000/svg', 'circle')
      this.setAttr()
      this.venn.appendChild(this.rect)
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
