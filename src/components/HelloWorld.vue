<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <upload-button title="Browse" :selectedCallback="fileSelectedFunc"></upload-button>
  </div>
</template>

<script>
import UploadButton from './UploadButton'

export default {
  name: 'HelloWorld',
  components: {
    UploadButton
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      file: null
    }
  },
  methods: {
    fileSelectedFunc (file) {
      console.log(file)
      this.file = file
    },
    submitForm () {
      let data = new FormData()
      data.append('file', this.file)
      let xhr = new XMLHttpRequest()

      xhr.addEventListener('readystatechange', function () {
        if (this.readyState === 4) {
          console.log(this.responseText)
        }
      })

      xhr.open('POST', 'http://localhost:8080/YOUR_API_ENDPOINT')
      console.log(xhr)
      xhr.send(data)
    }
  }
}
</script>