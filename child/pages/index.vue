<template>
  <div class="container">
    <div>
      <h1 class="title">
        child
      </h1>

      <h2>{{ message }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      message: ''
    }
  },

  mounted () {
    window.parent.postMessage({ mounted: true }, '*')
    window.addEventListener('message', this.handleMessage)
  },

  methods: {
    handleMessage (e) {
      console.log(222, `Parent message: ${e.data.message}`)
      this.message = e.data.message
    }
  }
}
</script>

<style>
.container {
  width: 100vw;
  min-height: 100vh;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
