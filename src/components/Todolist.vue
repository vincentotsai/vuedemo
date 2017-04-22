<template>
  <div class="todos">
    <h1>{{ title }}</h1>
    <p v-html="msg2"></p>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ol>
    	<li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">{{item.label}}</li >
    </ol>
  </div>
</template>

<script>
import Store from '../store.js'
// console.log(Store)
export default {
  name: 'todos',
  data () {
    return {
      title: 'My todo list.',
      msg2: '<span>Tip:</span>Tap Enter to add.',
      items: Store.fetch(),
      newItem: ''
    }
  },
  watch: {
  	 items: {
      handler: function (items) { Store.save(items) },
      deep: true
    }
  },
  methods:{
  	toggleFinish: function(item){
	  	item.isFinished = !item.isFinished
	  },
	  addNew:function(){
	  	this.items.push({
	  		label:this.newItem,isFinished:false
	  	})
	  	this.newItem=''
	  }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.finished {
	text-decoration: underline;
	cursor: pointer;
}
ol {
  list-style-type: none;
  padding: 0;
}

li {
  display: block;
  margin: 0 10px;
}
</style>
