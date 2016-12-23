<template>
  <div>
    <h2> CodeAholic </h2> <br>
      <codemirror :code='code' :options='editorOption' @changed='codeChange'></codemirror>
      <button @click='run()'> @run </button>
      <div class='console'>
          <p class='pconsole'>/**</p>
          <p class='pconsole indent'>* {{ stringCode }} </p>
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
      code: '',
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
      stringCode: 'Function out put will go here.'
    }
  },
  methods: {
    codeChange (newCode) {
      this.code = newCode
    },
    run () {
      let compile = document.createElement('SCRIPT')
      let textCode = document.createTextNode(this.code)
      compile.appendChild(textCode)
      document.body.appendChild(compile)
      console.log(document.body.appendChild(compile))
      this.stringCode = compile.appendChild(textCode)
      console.log('Text :: ', this.stringCode.constructor)
      console.log('Text :: ', this.stringCode)
      console.log('Text :: ', this.stringCode)
      // this.stringCode
      // $('.console').append('<p class=pconsole indent>' + challengeFunction() +' </p>')
    }
  },
  computed: {
    result () {
      /*eslint-disable */
      console.log(typeof this.stringCode)
      return this.stringCode
      /*eslint-enable */
    }
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
