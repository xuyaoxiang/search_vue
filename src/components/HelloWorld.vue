<template>
<div>
   <div>
  <span>标题内容:</span><input type="text" v-model="title_keyword">
  <button v-on:click="title_search">搜索</button>
  </div>

  <div>
  <span>标签:</span><input type="text" v-model="tag_keyword">
  <button v-on:click="tag_search">搜索</button>
  </div>

  <ul v-if="response && empty_data==false">
  <li v-for="item in response"><a :href="'http://www.xuyaoxiang.com/index.php/archives/'+item.cid+'.html'">{{item.title}}</a></li>
  </ul>
  <p v-if="empty_data && response==''">没有数据为空</p>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
    data () {
    return {
      title_keyword:'',
      tag_keyword:'',
      response:'',
      empty_data:false
    }
  },
  methods:{
    title_search (){
      var data_response=this;
      if(this.title_keyword==''){
        alert('关键字不能为空')
          return false;
      }
      this.axios.post('http://144.202.18.180/api/search', {keyword:this.title_keyword},{headers:{'Accept':'application/prs.search.v1+json'}})
  .then(function(response){
   data_response.tag_keyword='';
     if(response.data==''){
       data_response.response='';
        data_response.empty_data=true;
        return false;
    }
    data_response.empty_data=false;
    data_response.response=response.data;
  })
  .catch(function (error) {
    console.log(error);
  });
    },
    tag_search (){
      var data_response=this;
      if(this.tag_keyword==''){
        alert('关键字不能为空')
          return false;
      }
      this.axios.post('http://144.202.18.180/api/tag', {keyword:this.tag_keyword},{headers:{'Accept':'application/prs.search.v1+json'}})
  .then(function(response){
    data_response.title_keyword='';
    if(response.data==''){
      data_response.response='';
        data_response.empty_data=true;
        return false;
    }
    data_response.empty_data=false;
    data_response.response=response.data;
  })
  .catch(function (error) {
    console.log(error);
  });
    }

    
  },
  

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
