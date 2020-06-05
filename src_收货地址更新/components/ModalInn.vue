<template>
    <div>
        <Form ref="myform" :model="myform" :rules="ruleValidate" :label-width="140">
            <FormItem label="请选择省市县镇：" prop="pcas">
                <Dropdown trigger="custom" :visible="isShowDropDown" placement="bottom-start">
                    <a href="javascript:void(0)" @click="isShowDropDown=true">
                        <span v-if="s==''">请选择</span>
                        <span v-else>{{p}}{{c}}{{a}}{{s}}(点击修改)</span>
                        <Icon type="ios-arrow-down"></Icon>
                    </a>
                    <div></div>
                    <DropdownMenu slot="list" style="width:440px;height:220px">
                        <DropdownInn v-if="isShowDropDown" @sHan='zhenhan' :pcasObj='pcasObj' :origin_p='p' :origin_c='c' :origin_a='a' :origin_s='s' />
                        <div style="text-align: right;margin:10px;">
                            <Button type="primary" @click="isShowDropDown=false">关闭</Button>
                        </div>
                    </DropdownMenu>
                </Dropdown>
            </FormItem>
            <FormItem label="联系方式" prop="tel">
                <i-input v-model="myform.tel" placeholder="必须填写合法的手机号码"></i-input>
            </FormItem>
            <FormItem label="联系人" prop="n">
                <i-input v-model="myform.n" placeholder="请填写您的姓名（或昵称）"></i-input>
            </FormItem>
            <FormItem label="详细地址" prop="d">
                <i-input v-model="myform.d" placeholder="请填写您的详细地址"></i-input>
            </FormItem>
            <FormItem label="地址别名" prop="alias">
                <Row>
                    <i-col :span='6'>
                        <i-input v-model="myform.alias" placeholder=""></i-input>
                    </i-col>
                    <i-col :span='24-6'>
                        <Button v-for="item in ['家','学校','宿舍','公司']" :key="item" @click="aliasBtnHan(item)">{{item}}</Button>
                    </i-col>
                </Row>
            </FormItem>
        </Form>
    </div>
</template>

<script>
    import DropdownInn from './DropdownInn.vue';
    import axios from 'axios';
    export default {
        components: {
            DropdownInn
        },
        created() {
            axios.get('http://www.aiqianduan.com:56506/pcas').then(data => {
                this.pcasObj = data.data;
            })
        },
        data() {
            return {
                isShowDropDown: false,
                p: '',
                c: '',
                a: '',
                s: '',
                pcasObj: {},
                myform: {
                    tel: '',
                    n: '',
                    d: '',
                    alias: '',
                    pcas:''
                },
                ruleValidate: {
                    tel: [{
                            required: true,
                            message: '必须填写您的手机号码，方便与您取得联系！',
                            trigger: 'blur'
                        },
                        {
                            pattern: /^((\+|00)86)?((134\d{4})|((13[0-3|5-9]|14[1|5-9]|15[0-9]|16[2|5|6|7]|17[0-8]|18[0-9]|19[0-2|5-9])\d{8}))$/,
                            message: '必须填写合法的手机号码',
                            trigger: 'blur'
                        }
                    ],
                    n: [{
                        required: true,
                        message: '请填写您的姓名（或昵称）',
                        trigger: 'blur'
                    }],
                    alias: [{
                        required: true,
                        message: '请填写您的地址别名',
                        trigger: 'blur'
                    }],
                    pcas: [{
                        required: true,
                        message: '请填写您的地址',
                        trigger: 'blur'
                    }],
                    d: [{
                            required: true,
                            message: '请填写您的详细地址',
                            trigger: 'blur'
                        },
                        {
                            type: 'string',
                            min: 10,
                            max: 30,
                            message: '请填入10到30字之间',
                            trigger: 'blur',
                        }
                    ],
                }
            }
        },
        methods: {
            zhenhan(obj) {
                this.p = obj.p,
                    this.c = obj.c,
                    this.a = obj.a,
                    this.s = obj.s,
                    this.isShowDropDown = false;
                    this.$set(this.myform,'pcas','sssss')
            },
            aliasBtnHan(item) {
                this.myform = {
                    ...this.myform,
                    alias: item
                }
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>