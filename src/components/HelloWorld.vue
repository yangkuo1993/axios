<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
import Qs from 'qs'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    this.$http.all([this.demo1(), this.demo2(), this.demo3()]).then(this.$http.spread((one, two, three) => {
      console.log(one)
      console.log(two)
      console.log(three)
    }))
  },
  methods: {
    demo1 () {
      return this.$http.get('https://cnodejs.org/api/v1/topics', {
        params: {
          page: 1,
          limit: 10
        }
      })
    },
    demo2 () {
      return this.$http.get('https://cnodejs.org/api/v1/topics', {
        params: {
          page: 2,
          limit: 5
        }
      })
    },
    demo3 () {
      return this.$http({
        method: 'post',
        url: 'https://cnodejs.org/api/v1/topics',
        data: {
          page: 3,
          limit: 8
        },
        transformRequest: [function (data) {
          data = Qs.stringify(data)
          return data
        }]
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
