<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
    <hello></hello>
    <fine></fine>
    <h1 v-html="detail()"></h1>
    <input type="checkbox" v-model="use" id="r1">
    <div v-bind:class="{class2:use}">color</div>
    <div v-if="seen">v-if</div>
    <a v-bind:href="url">百度</a>
    <a v-on:click.prevent="doSomething" v-bind:href="url">click</a>
    <input v-model.lazy="name">
    <div>{{name | formatName }}</div>
    <div v-if="name === 0.5">
      >0.5
    </div>
    <div v-else-if="name === 'a'">
      a
    </div>
    <div v-else>
      c
    </div>
    <div v-show="use">show</div>
    <ul>
      <li v-for="site in sites">
        {{site.name}}
      </li>
      <template v-for="site in sites">
        <li>{{site.name}}</li>
        <li>-----------</li>
      </template>
      <li v-for="(value,key,index) in objectV">
        {{key}}:{{value}}:{{index}}
      </li>
      <li v-for="n in 10">
        {{n}}
      </li>
    </ul>
    <p>计算前:{{name}}</p>
    <p>计算后:{{namerevset}}</p>
    <input v-model="url"/>
    <input v-model="name" />
    <input v-model="objectV.age">
    <div v-bind:class="classObj"></div>
    <input @keyup.alt.67="doSomething"><!-- Alt + C -->
    <input @click.ctrl="doSomething"><!-- Ctrl + Click -->
    <p>单个复选框：</p>
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{checked}}</label>
    <p>多个复选框：</p>
    <input type="checkbox" id="x" value="x" v-model="checkedNames">
    <input type="checkbox" id="y" value="y" v-model="checkedNames">
    <input type="checkbox" id="z" value="z" v-model="checkedNames">
    <span>{{checkedNames}}</span>
    <select v-model="selected" name="fruit">
      <option value="">选择一个值</option>
      <option value="x">vx</option>
      <option value="y">vy</option>
      <option value="z">vz</option>
    </select>
    <div id="output">
      选择的网站是：{{selected}}
    </div>
  </div>
</template>

<script>
  import Hello from './components/Hello'
  import Fine from './components/Fine'
  export default{
  name: 'App',
  data:function(){
    return {
      checked:false,
      name:"xjnb",
      use: false,
      seen:false,
      url:"http://www.baidu.com",
      sites:[
        {name:'v1'},
        {name:'v2'}
      ],
      objectV:{
        name:'c1',
        age:3
      },
      checkedNames:[],
      selected:''
    }
  },
  components:{
    Hello,Fine
  },
  methods:{
    detail:function () {
      return "<a>"+this.name+"----fgnb </a>"
    },
    doSomething:function () {
      alert("click")
    },
    a:function (newV,oldV) {
      console.log(newV,oldV)
    }
  },
  filters:{
    formatName:function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  },
  computed:{
    namerevset: {
      get: function () {
        return this.name.split('').reverse().join('')
      },
      set: function (setvalue) {
        this.name = setvalue
      }
    },
    classObj:function () {
      return{
        base:true,
        bg1:this.use
      }
    }
  },
  watch:{
    url(newV,oldV){
      console.log(newV,oldV);
    },
    name:'a',
    'objectV.age':{
      handler(newV,oldV){
        console.log(newV,oldV);
      },
      immediate:false,
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
  .class1 {
    background: #444;
    color: #eee;
  }

  .class2 {
    background: #42b983;
    color: #eeeeee;
  }
  .base {
    width: 100px;
    height: 100px;
  }
  .bg1{
    background: #42b983;
  }
</style>
