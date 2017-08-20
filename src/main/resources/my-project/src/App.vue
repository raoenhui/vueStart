<template>
  <div id="app">
    <p>
      <!-- 使用 router-link 组件来导航. -->
      <!-- 通过传入 `to` 属性指定链接. -->
      <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
      <router-link to="/foo">Go to Foo</router-link>
      <router-link to="/bar">Go to Bar</router-link>
    </p>
    <router-view></router-view>
    <img src="./assets/logo.png">
    <ol>
      <li v-for="site in sites">
        {{ site.name }}
      </li>
    </ol>
    <div class="static"
         v-bind:class="{ active: isActive, 'text-danger': hasError }">
    </div>
    <div v-bind:class="classObject"></div>
    {{ message | capitalizeFirst }}<button v-on:click="reverseMessage">反转字符串</button>
    <div  v-bind:id="'list-' + id">vvvv</div>
    <hello></hello>

  </div>
</template>

<script>
  // 导入组件
  import Hello from './components/Hello';

  export default {
    name: 'app',
    components: {
      Hello
    },
    data () {
      return {
        message: 'abcd',
        id:1,
        sites: [
          { name: 'Runoob' },
          { name: 'Google' },
          { name: 'Taobao' }
        ],
        isActive: true,
        hasError: true
      }
    },
    methods:{
        reverseMessage: function () {
          this.message = this.message.split('').reverse().join('')
        }
    },
    filters:{
      capitalizeFirst:  (value)=> {
        if (!value) return ''
        value = value.toString()
        return value.charAt(0).toUpperCase() + value.slice(1)
      }
    },
    computed: {
      classObject: function () {
        return {
          active: this.isActive && !this.error,
          'text-danger': this.error && this.error.type === 'fatal',
        }
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.active {
  width: 100px;
  height: 100px;
  background: green;
}
.text-danger {
  background: red;
}
</style>
