<template>
<div class="container col-2 px-2 py-2 mx-auto my-5">
    <div class="result text-right px-3 py-3">
        {{result || 0}}
    </div>
    <div class="buttons d-flex flex-wrap">
        <div class="col-3 operation" v-for="n in buttons" :key="n">
       <div class="orange py-2 my-1"  @click="action(n)">
           {{n}}
       </div>
    </div>
    </div>
</div>
</template>
<script>
export default {
  name: 'Calculator',
  data(){
      return{
         result:"",
         buttons:["CE","","<-","/",1,2,3,"*",4,5,6,"+",7,8,9,"-",0,"="],
         previous:"",
         operator:null
      }
  },
  methods:{
      action(n){
          if(!isNaN(n)){
              this.result+=n
          }
          if(n==="CE"){
              this.result="";
          }
          if([`/`,`*`,`+`,`-`].includes(n)){
              this.operator=n
             this.previous=this.result
           this.result=""
          }
            if(n==="="){
                
                this.result=eval(
                    this.previous + this.operator + this.result
                )
                this.previous="";
                this.operator=null
          }
          if(n==="<-"){
              let res= Array.from(this.result)
              res.pop()
              let answer=""
             for(let el of res){
                
                 answer+= el
             }
             this.result=""
             this.result=answer
          }
      }
  }
}
</script>
<style scoped>
.buttons{
    cursor: pointer;
}
.operation:nth-child(2) div{
    display: none;
}
.operation:nth-child(1) div{
    background: red!important;
    width:100px;
    z-index: 999;
}
.operation:nth-child(3) div{
    background: blue!important
}
.operation:nth-child(18) div{
    background: green!important;
    width: 100px;
    align-self: end;
}
.container{
    background: brown;
 
    border-radius: 20px;
}
.result{
    background: white;
    border-radius: 20px;
}
.orange{
    background: orange;
    border-radius: 5px;
    color: white;

}
.red{
    background: red;
}
</style>