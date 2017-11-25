<template>
  <div id="app">
    <h1>Bộ cuyển dổi Tiếq Việt</h1>
    <textarea
      v-model="message"
      placeholder="Gõ tiếng Việt vào đây nào các bạn"
      @input="convert"></textarea>
    <pre class="result">{{ convertedMessage }}</pre>
    <button @click="copy">Copy</button>

    <p class="copyright">
      Một dự án nhỏ của <a href="https://phanan.net">Phan An</a>.
      Sử dụng <a href="https://vi.vuejs.org">Vue.js</a> và
        module <a href="https://github.com/phanan/tieqviet">tieqviet</a>.
      Mã nguồn trên <a href="https://github.com/phanan/tieqviet-demo">GitHub</a>.<br/>
      <a href="https://thanhnien.vn/giao-duc/khi-tieng-viet-duoc-viet-thanh-tieq-viet-903068.html">Tại sao lại có cái này?</a>
    </p>

    <textarea class="target" ref="copyArea" v-model="convertedMessage"></textarea>
  </div>
</template>

<script>
import tieqViet from 'tieqviet'
import { debounce } from 'lodash'

export default {
  name: 'app',
  data () {
    return {
      message : `Trăm năm trong cõi người ta
Chữ tài chữ mệnh khéo là ghét nhau
Trải qua một cuộc bể dâu
Những điều trông thấy mà đau dạ dày
Ta đi trên trái đất này
Bốn phương vô sản dạ dày đều đau
Lớp cha trước, lớp con sau
Đã thành đồng chí, cùng đau dạ dày`,
      convertedMessage: ''
    }
  },

  mounted () {
    this.convert()
  },

  methods: {
    convert: debounce(function () {
      this.convertedMessage = tieqViet(this.message)
    }, 200),

    copy () {
      this.$refs.copyArea.select()
      document.execCommand('copy')
      this.$refs.copyArea.blur()
    }
  }
}
</script>

<style lang="scss">
body, html {
  font-size: 14px;
  font-family: 'Open Sans', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding-top: 15px;
  line-height: 1.6;
}

a {
  color: #b74444;
  text-decoration: none;
}

#app {
  width: 500px;
  margin: 0 auto;
}

textarea {
  width: 100%;
  height: 150px;
  border: 1px solid #ccc;
  font-family: 'Open Sans', Helvetica, Arial, sans-serif;
  font-size: 1rem;
  padding: 8px;
}

.result {
  width: 100%;
  margin: 0 auto;
  margin-top: 18px;
  background: #f1f1f1;
  border-radius: 5px;
  padding: 8px;
  font-family: 'Open Sans', Helvetica, Arial, sans-serif;
  white-space: pre-wrap
}

.copyright {
  font-size: .9rem;
  margin-top: 50px;
  color: #666;
}

.target {
  width: 1px;
  height: 1px;
  position: fixed;
  bottom: 0;
  opacity: 0;
}
</style>
