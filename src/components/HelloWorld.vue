<template>
  <div class="hello">
    <a @click="next()">
      <img id ="logo" :src="'./logo.png'"/>
    </a>
    <h2>小巴的豐盛日記</h2>
    <ul>
      <li v-for = "i in items.slice().reverse()" :key="i">
        <a @click="read(i)">* {{i}}</a>
      </li>
    </ul>
    <router-link to="/about">
      <img class="living_room" src="../assets/living_room.jpg">
    </router-link>
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
      items: ['豐盛日記 20210222(一)', '豐盛日記 20210223(二)', '豐盛日記 20210224(三)', '豐盛日記 20210225(四)', '豐盛日記 20210226(五)', '豐盛日記 20210228(日)', '豐盛日記 20210301(一)', '豐盛日記 20210302(二)', '豐盛日記 20210303(三)', '豐盛日記 20210304(四)', '豐盛日記 20210305(五)', '豐盛日記 20210306(六)', '豐盛日記 20210307(日)', '豐盛日記 20210308(一)', '豐盛日記 20210309(二)', '豐盛日記 20210310(三)', '豐盛日記 20210311(四)', '豐盛日記 20210312(五)', '豐盛日記 20210313(六)', '豐盛日記 20210314(日)', '豐盛日記 20210315(一)', '豐盛日記 20210316(二)', '豐盛日記 20210317(三)', '豐盛日記 20210318(四)', '豐盛日記 20210319(五)', '豐盛日記 20210320(六)', '豐盛日記 20210321(日)', '豐盛日記 20210322(一)', '豐盛日記 20210323(二)', '豐盛日記 20210324(三)', '豐盛日記 20210325(四)', '豐盛日記 20210326(五)', '豐盛日記 20210327(六)', '豐盛日記 20210328(日)', '豐盛日記 20210329(一)', '豐盛日記 20210330(二)']
    }
  },
  methods: {
    next() {
      let index = this.items.indexOf(this.item)
      let n = (index - 1 + this.items.length) % this.items.length
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
    this.$http.get(this.items[this.items.length - 1]).then((response) => {
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
  box-shadow: 0px 5px 5px 0px #9B8F99;
}

.living_room {
  width: 30vmin;
  float: left;
  border-radius: 50px;
  margin-left: 15vmin;
  margin-right: 1em;
}

ul {
  color: black;
  padding: 1em;
  height: 10vmax;
  width: 33vmax;
  margin: 1em auto;
  background-color: white;
  overflow-y: scroll;
  box-shadow: 0px 5px 5px 0px #9B8F99;
  border-radius: 15px 0 0 15px;
}

li {
  display: block;
  margin: 0 10px;
  text-decoration: underline;
}

a {
  font-weight: bold;
  cursor: pointer;
  color: blue;
}

div.d {
  width: 65vw;
  max-width: 680px;
  margin: 0 auto;
  white-space: pre-line;
  text-align: left;
  font-size: 16px;
  padding: 1em;
  background-color: white;
  box-shadow: 0px 5px 5px 0px #9B8F99;
  border-radius: 15px;
  line-height: 2;

}

div.d::first-line {
  color: blue;
  font-size: 2em;
  font-weight: bolder;
}

@media screen and (max-width: 420px) {
  div.d::first-line {
    color: blue;
    font-size: 1em;
  }

  div.d {
    width: 85vw;
  }

  #logo {
    margin: .5em;
  }
}

</style>
