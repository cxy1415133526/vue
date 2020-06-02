<template>
    <div class="wrapDrop">
        <div class="dt">
            <div class="hd">
                <span  :class="{'cur':nowshow=='p'}" @click="hd_Han('p')" >
                    <em v-if="p!=''">{{p}}</em>
                    <em v-else>请选择省份(直辖市)</em>
                </span>
                <span :class="{'cur':nowshow=='c'}" @click="hd_Han('c')"  >
                     <em v-if="c!=''">{{c}}</em>
                    <em v-else>请选择市</em>                    
                </span>
                <span  :class="{'cur':nowshow=='a'}" @click="hd_Han('a')"  >
                      <em v-if="a!=''">{{a}}</em>
                    <em v-else>请选择县</em>
                    {{a}}
                </span>
                <span :class="{'cur':nowshow=='s'}" @click="hd_Han('s')" >
                      <em v-if="s!=''">{{s}}</em>
                    <em v-else>请选择镇</em>
                    {{s}}
                </span>
            </div>
            <p v-if="nowshow=='p'">
                <a href="javascript:" class="ys" v-for="(v,p) in pacsobj" :key="p" @click="pHan(p)">{{p}}</a>
            </p>
            <p v-if="nowshow=='c'">
                <a href="javascript:" class="ys" v-for="(v,c) in pacsobj[p]" :key="c" @click="cHan(c)">{{c}}</a>
            </p>
            <p v-if="nowshow=='a'">
                <a href="javascript:" class="ys" v-for="(v,a) in pacsobj[p][c]" :key="a" @click="aHan(a)">{{a}}</a>
            </p>
            <p v-if="nowshow=='s'">
                <a href="javascript:" class="ys" v-for="s in pacsobj[p][c][a]" :key="s" @click="sHan(s)">{{s}}</a>
            </p>
         
          
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                pacsobj: {},
                nowshow:"p",
                p:"",
                c:"",
                a:"",
                s:"",
                

            }
        },
        created(){
            axios.get('http://www.aiqianduan.com:56506/pcas').then(data=>{
                this.pacsobj=data.data;    
                console.log(data.data);
                                                   
            })
        },
        methods:{
            pHan(p){
                
                this.p=p;
                this.nowshow='c';
                this.c='';
                this.a='';
                this.s='';
            },
            cHan(c){
              this.c=c;
              this.nowshow='a';
              this.a='';
              this.s='';
            },
            aHan(a){
              this.a=a;
              this.nowshow='s';
              this.s=''; 
            },
            sHan(s){
                this.s=s;
                this.$emit('sHan',{
                    p:this.p,
                    c:this.c,
                    a:this.a,
                    s:this.s
                })
            },
            hd_Han(m){
                this.nowshow=m;
            }
          
        }
    }
</script>

<style lang="less" scoped>
    .wrapDrop{
        margin: 10px 10px;
    }
    .hd{
       height: 25px;
       border-bottom: 1px solid #ccc;
       margin-bottom: 10px;
       span{
           float: left;
           padding:0 10px;
           border: 1px solid #eee;
           border-bottom:none;
           font-size: 12px;
           color: white;
           cursor: pointer;
           background: -webkit-linear-gradient(bottom left,rgba(255, 0, 0, 0.692),rgba(33, 184, 189, 0.856));
           &.cur{
               background: -webkit-linear-gradient(top right,gold,white);
               color: red;
           }
           em{
               font-style:normal;
           }
       }
    }
    .ys{
        margin-right: 10px;
        float: left;
    }
</style>