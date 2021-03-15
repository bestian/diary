<template>
  <div class="hello">
    <a @click="next()">
      <img id ="logo" :src="'./logo.png'"/>
    </a>
    <h3>小巴的豐盛日記</h3>
    <ul>
      <li v-for = "i in items" :key="i">
        <a @click="read(i)">* {{i}}</a>
      </li>
    </ul>
    <div class="d" v-html="d">
    </div>
    <a @click="next()">
      <img id ="logo" :src="'./logo.png'"/>
    </a>
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
      d: '',
      item: '豐盛日記 20210222(一)',
      items: ['豐盛日記 20210222(一)', '豐盛日記 20210223(二)', '豐盛日記 20210224(三)', '豐盛日記 20210225(四)', '豐盛日記 20210226(五)', '豐盛日記 20210228(日)', '豐盛日記 20210301(一)', '豐盛日記 20210302(二)', '豐盛日記 20210303(三)', '豐盛日記 20210304(四)', '豐盛日記 20210305(五)', '豐盛日記 20210306(六)', '豐盛日記 20210307(日)', '豐盛日記 20210308(一)', '豐盛日記 20210309(二)', '豐盛日記 20210310(三)', '豐盛日記 20210311(四)', '豐盛日記 20210312(五)', '豐盛日記 20210313(六)', '豐盛日記 20210314(日)', '豐盛日記 20210315(一)']
    }
  },
  methods: {
    next() {
      let index = this.items.indexOf(this.item)
      let n = (index + 1) % this.items.length
      this.read(this.items[n])
    },
    read(k) {
      this.item = k
      this.$http.get('./' + k).then((response) => {
        // console.log(response.data)
        this.d = response.data
      })
    }
  },
  mounted () {
    this.$http.get('./豐盛日記 20210222(一)').then((response) => {
      // console.log(response.data)
      this.d = response.data
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#logo {
  margin: 2em;
  width: 10vw;
  border-radius: 30px;
}

ul {
  color: black;
  list-style-type: decimal;
  padding: 2em;
  height: 10vmax;
  width: 33vmax;
  margin: 1em auto;
  overflow-y: scroll;
}

li {
  display:list-item;
  list-style-position:outside;
  display: block;
  margin: 0 10px;
}
a {
  font-weight: bold;
  cursor: pointer;
  color: blue;
}

div.d {
  width: 80vw;
  margin: 0 auto;
  white-space: pre-line;
  text-align: left;
}

div.d::first-line {
  font-size: 2em;
  font-weight: bolder;
}

</style>
