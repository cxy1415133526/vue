<template>
  <div class="wrap">
        <CheckboxGroup v-model="color"  >
        <Checkbox :label="item" :key="index" v-for="(item,index) in ['红','绿','蓝','白','黑']">
            <span>{{item}}</span>
        </Checkbox>        
      </CheckboxGroup>
           
      <Table :columns="cols" :data="data" ></Table>
    <div class="pagebox">
       <Page :total="total"  :current='current' :page-size='10'  @on-change='changePage' prev-text='上一页' next-text='下一页' show-sizer />
    </div>
      
  </div>
</template>

<script>
import axios from 'axios';
  export default {
    created(){
     this.loadData()
    },
      data() {
        return {
          current:1,
          total:0,
         
          cols: [
          
            // 一行数据，解构这个row，得到这一条数据
            {'title':'车辆图片','key':'img',render(h,{row}){
              console.log(row);
              
              return h('div',[h('img',{
                attrs:{
                  src:`http://aiqianduan.com:56506/images/carimages_small/${row.id}/view/${row.img}`
                }
              })])
            }},
            {'title':'编号','key':'id'},
            {'title':'品牌','key':'brand'},
            {'title':'车系','key':'series'},
            {'title':'颜色','key':'color'},            
            {'title':'排量','key':'engine'},            
            {'title':'尾气','key':'exhaust'},            
            {'title':'燃料','key':'fuel'},            
          ],
          data:[],
          color:[]

        }
      },
      methods:{
        loadData(){
          axios.get('http://www.aiqianduan.com:56506/cars?page='+this.current+'&color='+this.color.join('v')).then(data=>{
            this.data=data.data.results;
            this.total=data.data.total;
          });
      
           
        },
        changePage(current){
          this.current=current;
          this.loadData();
        }
      },
      watch:{
        color(){
          this.current=1;
          this.loadData();
        }
      }
  }
</script>

<style lang="less" scoped>
    .wrap{
      width:1000px;
      margin: 40px auto;
    }
    .pagebox{
      margin-top: 20px;
    }
    
   
</style>