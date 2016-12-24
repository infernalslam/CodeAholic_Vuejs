<template>
  <div>
    <h2> CodeAholic </h2> <br>
      <codemirror :code='code' :options='editorOption' @changed='codeChange'></codemirror>
      <button @click='run()'> @run </button>
      <!-- <codemirror :code='strCode' :options='editorOption'></codemirror> -->
      <div class='console'>
          <p class='pconsole'>/**</p>
          <p class='pconsole indent' id='demo' >{{ strCode }}</p>
          <p class='pconsole indent'>* /</p>
      </div>
  </div>
</template>

<script>
import { codemirror } from 'vue-codemirror'
export default {
  name: 'app',
  components: {
    codemirror
  },
  data () {
    return {
      code: `( function ( ) {
        let data = [ { name: 'Tak'}, { name: '💞' }, { name: 'Mint'} ]
        return data.map(item => item.name)
}( ) )`,
      editorOption: {
        mode: 'text/javascript',
        theme: 'base16-dark',
        tabSize: 2,
        lineNumbers: true,
        line: true,
        keyMap: 'sublime',
        extraKeys: { 'Ctrl': 'autocomplete' },
        foldGutter: true,
        gutters: ['CodeMirror-linenumbers', 'CodeMirror-foldgutter'],
        styleSelectedText: true,
        highlightSelectionMatches: { showToken: /\w/, annotateScrollbar: true }
      },
      strCode: 'Function out put will go here.'
    }
  },
  methods: {
    codeChange (newCode) {
      this.code = newCode
    },
    run () {
      console.log(this.code)
      /*eslint-disable */
      eval(`this.strCode =` + this.code)
      console.log(this.strCode)
      /*eslint-enable */
    }
  },
  computed: {
  },
  mounted () {
    this.run()
  }
}
</script>

<style>
@font-face {
  font-family: 'San Francisco';
  font-weight: 500;
  src: url('https://applesocial.s3.amazonaws.com/assets/styles/fonts/sanfrancisco/sanfranciscodisplay-ultralight-webfont.woff');
}
* {
    font-family: 'San Francisco';
    font-size: 20px;
}
.style-code {
  position: absolute;
  width: 100vh;
  height: 100vh;
}
.pconsole {
    margin-left:10px;
    text-align: left;
    color:#e6e6e6;
}
.indent {
    text-indent: 10px;
}
.console {
    padding-top:10px;
    padding-bottom:10px;
    width:90%;
    min-height:100px;
    background:#1a1a1a;
    margin:auto;
    margin-top:20px;
    border-radius:5px;
}
</style>
