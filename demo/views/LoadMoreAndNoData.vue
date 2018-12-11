<template>
  <scroller
      :on-infinite="infinite"
      ref="my_scroller"
      loadingLayerColor="red"
      noDataText="已经到底啦!">
    <div>1</div>
    <div class="row" v-for="(item, index) in items" :key="index">
      {{ item }}
    </div>
  </scroller>
</template>
<script>
  import NavBar from './NavBar.vue'

  export default {
    components: {
      NavBar
    },

    data () {
      return {
        items: []
      }
    },

    mounted() {
      for (let i = 1; i <= 20; i++) {
        this.items.push(i + ' - keep walking, be 2 with you.')
      }
      this.top = 1
      this.bottom = 20
    },

    methods: {
      infinite(done) {
        if (this.bottom >= 30) {
          setTimeout(() => {
            done(true)
          }, 1500)
          return;
        }

        setTimeout(() => {
          let start = this.bottom + 1
          for (let i = start; i < start + 10; i++) {
            this.items.push(i + ' - keep walking, be 2 with you.')
          }
          this.bottom = this.bottom + 10;
          setTimeout(() => {
            done()
          })
        }, 1500)
      }
    }
  }
</script>
