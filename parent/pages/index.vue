<template>
  <div class="container">
    <div>
      <h1 class="title">
        parent
      </h1>

      <button @click="btnClick">button</button>
      <div>
        <iframe
          ref="child"
          class="iframe"
          src="http://localhost:4001/"
          v-show="isIframe"
        ></iframe>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isIframe: false
    }
  },

  mounted() {
    window.addEventListener('message', this.iframeMessage)
  },

  computed: {
    iframe() {
      return this.$refs.child.contentWindow
    }
  },

  methods: {
    iframeMessage (e) {
      if (e.data.mounted) {
        this.isIframe = true;
        console.log(111, 'Iframe Page Mounted');
        this.iframe.postMessage({
          message: 'Message from parent'
        }, '*');
      }
    },

    onLoad () {
      // console.log(111, 'onLoad');
    },

    onIframeLoad() {
      // console.log(222, 'onIframeLoad');
    },

    btnClick () {
      this.iframe.postMessage({
        message: 'Button click from parent'
      }, '*');
    }
  }
}
</script>

<style>
  .iframe {
    width: 100%;
    margin-top: 30px;
    height: 300px;
    border: 1px solid red !important;
  }
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

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
