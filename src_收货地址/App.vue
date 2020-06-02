<template>
    <div class="wrap">
        <Row :gutter='16'>
            <i-col :span="6" v-for="(item,index) in arr" :key="index">
                <Card style="width:250px;height:160px">
                    <p slot="title">
                        <b>{{item.alias}}</b>
                    </p>
                    <a href="#" slot="extra" style="margin-right:10px" @click="del(index)">删除</a>
                    <a href="#" slot="extra" @click="updataItem(item)">修改</a>
                    <p>地址：{{item.p}}{{item.c}}{{item.a}}{{item.s}}{{item.d}}</p>
                    <p>收货人:{{item.n}}</p>
                    <p>Tel:{{item.tel}}</p>
                </Card>
            </i-col>
            <i-col :span="6">
                <Card style="height:160px;text-align:center;font-size:80px;line-height:120px">
                    <span class="plus" @click="isShowModal=true" style="cursor:pointer">+</span>
                </Card>
            </i-col>
            <Modal v-model="isShowModal" title="增加收货地址" @on-ok="ok"
        @on-cancel="cancel">>
                <b>请选择省市县镇</b>
                <Dropdown trigger="custom" :visible="isShowDropdown" style="margin-left: 20px;" placement="bottom-start">
                    <a href="javascript:void(0)" @click="isShowDropdown=true">
                        请选择省市县镇
                        <Icon type="ios-arrow-down"></Icon>
                    </a>
                     <Input v-model="p" placeholder="省（直辖市）" clearable style="width: 80px" />                                        
                     <Input v-model="c" placeholder="市" clearable style="width: 80px;font-size:0px" />
                     <Input v-model="a" placeholder="县" clearable style="width: 80px;font-size:0px" />
                     <Input v-model="s" placeholder="镇" clearable style="width: 80px;font-size:0px" />
                  
                    <DropdownMenu slot="list" style="width:400px;height:200px">
                        <DropdownMenuIn  @sHan="changesHan" />
                        <div style="text-align: right;margin:10px;">
                            <Button type="primary" @click="isShowDropdown=false">关闭</Button>
                        </div>
                    </DropdownMenu>
                </Dropdown>
            </Modal>
            <Modal v-model="isShowModal1" title="修改收货地址" @on-ok="ok1"
        @on-cancel="cancel1">>
                <b>请选择省市县镇</b>
                <Dropdown trigger="custom" :visible="isShowDropdown" style="margin-left: 20px;" placement="bottom-start">
                    <a href="javascript:void(0)" @click="isShowDropdown=true">
                        请选择省市县镇
                        <Icon type="ios-arrow-down"></Icon>
                    </a>
                     <Input v-model="p" placeholder="省（直辖市）" clearable style="width: 80px" />                                        
                     <Input v-model="c" placeholder="市" clearable style="width: 80px;font-size:0px" />
                     <Input v-model="a" placeholder="县" clearable style="width: 80px;font-size:0px" />
                     <Input v-model="s" placeholder="镇" clearable style="width: 80px;font-size:0px" />
                  
                    <DropdownMenu slot="list" style="width:400px;height:200px">
                        <DropdownMenuIn  @sHan="changesHan" />
                        <div style="text-align: right;margin:10px;">
                            <Button type="primary" @click="isShowDropdown=false">关闭</Button>
                        </div>
                    </DropdownMenu>
                </Dropdown>
            </Modal>
        </Row>
    </div>
</template>

<script>
    import axios from 'axios';
    import DropdownMenuIn from './components/DropdownMenuIn.vue';
    export default {
        components:{
            DropdownMenuIn
        },
        data() {
            return {
                isShowModal: false,
                isShowModal1:false,
                isShowDropdown:false,
                arr: [],
                p:"",
                c:"",
                a:"",
                s:""
            }
        },
        created() {
            axios.get('http://www.aiqianduan.com:56506/shdz/sudas').then(data => {
                this.arr = data.data;
            })
        },
        methods:{
            changesHan(obj){
                this.p=obj.p;
                this.c=obj.c;
                this.a=obj.a;
                this.s=obj.s;
                this.isShowDropdown=false;
            },
            ok () {

                this.$Message.info('添加成功');
            },
            cancel () {
                this.$Message.info('取消添加');
            },
            ok1 () {

                this.$Message.info('修改成功');
            },
            cancel1 () {
                this.$Message.info('取消修改');
            },
            del(index){
                this.arr.splice(index,1)
            },
            updataItem(item){                
                this.isShowModal1=true;
                this.p=item.p;
                this.c=item.c;
                this.a=item.a;
                this.s=item.s;
            }
        }
    }
</script>

<style lang="less" scoped>
    .wrap {
        width: 1000px;
        margin: 40px auto;
        .plus:hover {
            color: orange;
            
        }
    }
    DropdownMenuIn{
        width: 150px;
    }
</style>