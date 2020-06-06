<template>
    <div class="wrap">
        <Row :gutter='16'>
            <i-col :span='6' v-for="(item,index) in arr" :key="index">
                <Card style="height:160px">
                    <p slot="title">
                        <b>{{item.alias}}</b>
                    </p>
                    <p slot="extra">
                        <a href="#" style="margin-right:10px">修改</a>
                        <a href="#">删除</a>
                    </p>
                    <div>
                        <b>地址：</b> {{item.p}}{{item.c}}{{item.a}}{{item.s}}{{item.d}}
                    </div>
                    <div>
                        <b>收货人：</b> {{item.n}}
                    </div>
                </Card>
            </i-col>
            <i-col :span='6'>
                <Card style="height:160px;position:relative" v-if="arr.length != 4">
                    <div class="jiahao" @click="isShowModal=true"></div>
                </Card>
            </i-col>
        </Row>
        <Modal :value="isShowModal" title="增加收货地址" :width="700">
            <ModalInn ref="ModalInn" />
            <p slot="footer">
                <Button @click="isShowModal=false">取消</Button>
                <Button type="primary" @click="okHan">确定</Button>
            </p>
        </Modal>
    </div>
</template>

<script>
    import ModalInn from './components/ModalInn.vue';
    import axios from 'axios';
    export default {
        components: {
            ModalInn
        },
        data() {
            return {
                arr: [],
                isShowModal: false,
            }
        },
        created() {
            axios.get('http://www.aiqianduan.com:56506/shdz/苏打水5').then(data => {
                this.arr = data.data;
            })
        },
        methods: {
            okHan() {
                this.$refs.ModalInn.$refs.myform.validate((data) => {
                    if (data) {
                        const {
                            p,
                            c,
                            a,
                            s
                        } = this.$refs.ModalInn;
                        const {
                            tel,
                            d,
                            n,
                            alias
                        } = this.$refs.ModalInn.myform;
                         this.isShowModal=false;
                         axios.post('http://www.aiqianduan.com:56506/shdz/苏打水5',{
                             p,c,a,s,d,n,alias,tel
                         }).then(data=>{
                             alert(data.data);
                         })
                    }
                });
            },
        }
    }
</script>

<style lang="less" scoped>
    .wrap {
        .jiahao {
            position: absolute;
            top: 50%;
            left: 50%;
            margin-left: -40px;
            width: 80px;
            height: 80px;
            margin-top: -40px;
            background: url(/images/jiahao.svg);
            &:hover {
                background: url(/images/jiahao1.svg);
            }
        }
    }
</style>