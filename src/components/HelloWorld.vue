<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>
      {{
        !onLine
          ? 'You are Offline...'
          : showBackOnline
          ? 'Back Online...'
          : message
      }}
    </h2>
    <h3>Links of Most Popular PWA examples</h3>
    <ul>
      <li><a href="https://www.bmw.com/en/index.html" target="_blank" rel="noopener">BMW</a></li>
      <li><a href="https://www.starbucks.com" target="_blank" rel="noopener">Starbucks</a></li>
      <li><a href="https://www.pinterest.ca" target="_blank" rel="noopener">Pinterest</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      message: 'Welcome to Vue!',
      onLine: navigator.onLine,
      showBackOnline: false
    }
  },
  methods: {
    doSomething() {
      alert('Hello!')
    },
    updateOnlineStatus(e) {
      const { type } = e
      this.onLine = type === 'online'
    }
  },
  watch: {
    onLine(v) {
      if (v) {
        this.showBackOnline = true
        setTimeout(() => {
          this.showBackOnline = false
        }, 1000)
      }
    }
  },
  mounted() {
    window.addEventListener('online', this.updateOnlineStatus)
    window.addEventListener('offline', this.updateOnlineStatus)
  },
  beforeDestroy() {
    window.removeEventListener('online', this.updateOnlineStatus)
    window.removeEventListener('offline', this.updateOnlineStatus)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: circle;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
}
a,button {
  color: #42b983;
}

button {
  background: none;
  border: solid 1px;
  border-radius: 2em;
  font: inherit;
  padding: 0.75em 2em;
  margin-bottom: 1rem;
  margin-left: auto;
  margin-right: auto;
  display: block;
}
</style>
