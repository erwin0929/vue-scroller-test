<template>
  <div>
    <scroller :on-refresh="refresh" refreshText="下拉加载更多">
      <div v-for="(item, index) in items" class="row">
        {{ item }}
      </div>
    </scroller>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        items: []
      }
    },

    mounted() {
      for (let i = 1; i <= 10; i++) {
        this.items.push(i)
      }

      this.top = 1
      this.bottom = 20
    },

    methods: {
      refresh(done) {
        setTimeout(() => {
          let start = this.top - 1

          for (let i = start; i > start - 10; i--) {
            this.items.splice(0, 0, i + ' - keep walking, be 2 with you.')
          }

          this.top = this.top - 10;

          done()
        }, 500)
      }
    }
  }
</script>

<style scoped>
  .row::before{
    content: '这是第';
  }
  .row::after{
    content: '条';
  }
</style>