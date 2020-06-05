<template>
    <div class="ddinn">
        <div v-if="Object.keys(pcasObj).length !=0">
            <div class="hd">
                <span :class="{'cur':nowshow=='p'}" @click="pHan">
                    {{p==''?'请选择省/市':p}}
                </span >
                <span  v-if="p!=''" :class="{'cur':nowshow=='c'}" @click="cHan">
                    {{c==''?'请选择城市':c}}
                </span >
                <span v-if="c!=''" :class="{'cur':nowshow=='a'}" @click="aHan" >
                    {{a==''?'请选择县':a}}
                </span>
                <span v-if="a!=''" :class="{'cur':nowshow=='s'}" @click="sHan">
                    {{s==''?'请选择镇':s}}
                </span>
            </div>
            <div class="bd">
                <div class="p_box" v-if="nowshow=='p'">
                    <RadioGroup v-model="nowshowType" type="button" size="small">
                        <Radio label="pinyin">按拼音</Radio>
                        <Radio label="quyu">按区域</Radio>
                    </RadioGroup>
                    <div class="p_bd_box">
                        <div v-if="nowshowType=='pinyin'">
                            <div v-for="(v,k) in data1" :key="k" class="contentRow">
                                <b>{{k}}:</b>
                                <a v-for="p in v" :key="p" @click="choose_p_Han(p)">{{p}}</a>
                            </div>
                        </div>
                        <div v-if="nowshowType=='quyu'">
                            <div v-for="(v,k) in data2" :key="k" class="contentRow">
                                <b>{{k}}:</b>
                                <a v-for="p in v" :key="p" @click="choose_p_Han(p)">{{p}}</a>
                            </div>
                        </div>
                    </div>
                </div>
                <div v-if="nowshow=='c'">
                    <div class="contentRow">
                        <a v-for='(v,c) in pcasObj[p]' :key="c" @click="choose_c_Han(c)">
                            {{c}}
                        </a>
                    </div>
                </div>
                <div v-if="nowshow=='a'">
                    <div class="contentRow">
                        <a v-for='(v,a) in pcasObj[p][c]' :key="a" @click="choose_a_Han(a)">
                            {{a}}
                        </a>
                    </div>
                </div>
                <div v-if="nowshow=='s'">
                    <div class="contentRow">
                        <a v-for='s in pcasObj[p][c][a]' :key="s" @click="choose_s_Han(s)">
                            {{s}}
                        </a>
                    </div>
                </div>
            </div>
        </div>
        <div v-else>
            <Spin fix>
                <Icon type="ios-loading" size=18 class="demo-spin-icon-load"></Icon>
                <div>Loading</div>
            </Spin>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['pcasObj', 'origin_p', 'origin_c', 'origin_a', 'origin_s'],
        data() {
            return {
                p: this.origin_p || '',
                c: this.origin_c || '',
                a: this.origin_a || '',
                s: this.origin_s || '',
                nowshow: this.origin_s == '' ? 'p' : 's',
                nowshowType: 'pinyin',
                data1: {
                    'A': ['安徽省'],
                    'B': ['北京市'],
                    'C': ['重庆市'],
                    'F': ['福建省'],
                    'G': ['甘肃省', '广东省', '广西壮族自治区', '贵州省'],
                    'H': ['海南省', '河北省', '河南省', '黑龙江省', '湖北省', '湖南省'],
                    'J': ['江西省', '吉林省', '江苏省'],
                    'L': ['辽宁省'],
                    'N': ['内蒙古', '宁夏回族'],
                    'Q': ['青海省'],
                    'S': ['山西省', '山东省', '陕西省', '上海市', '四川省'],
                    'T': ['天津市'],
                    'X': ['西藏自治区', '新疆维吾尔自治区'],
                    'Y': ['云南省'],
                    'Z': ['浙江省']
                },
                data2: {
                    '东北': ['黑龙江省', '吉林省', '辽宁省', '内蒙古'],
                    '华北': ['北京市', '天津市', '河北省'],
                    '西南': ['西藏自治区', '云南省', '广西壮族自治区', '贵州省', '四川省', '重庆市'],
                    '东南': ['福建省', '江西省'],
                    '中原': ['河南省', '山西省', '陕西省', '江苏省', '湖北省', '湖南省', '安徽'],
                    '华东': ['山东省', '上海市', '浙江省'],
                    '西北': ['新疆维吾尔自治区', '青海省', '宁夏回族', '甘肃省'],
                    '华南': ['海南省', '广东省'],
                }
            };
        },
        methods: {
            choose_p_Han(p) {
                this.p = p;
                this.nowshow = 'c'
            },
            choose_c_Han(c) {
                this.c = c
                this.nowshow = 'a'
            },
            choose_a_Han(a) {
                this.a = a;
                this.nowshow = 's'
            },
            choose_s_Han(s) {
                this.s = s;
                this.$emit('sHan', {
                    p: this.p,
                    c: this.c,
                    a: this.a,
                    s: this.s,
                });
            },
            pHan() {
                this.nowshow = 'p';
                this.c = '';
                this.a = '';
                this.s = '';
            },
            cHan() {
                this.nowshow = 'c';
                this.a = '';
                this.s = '';
            },
            aHan() {
                this.nowshow = 'a';
                this.s = '';
            },
            sHan() {
                this.nowshow = 's';
            },
        }
    }
</script>

<style lang="less" scoped>
    .ddinn {
        width: 440px;
        height: 180px;
        padding-left: 5px;
        .hd {
            height: 30px;
            border-bottom: 1px solid #ccc;
            padding: 0 10px;
            span {
                font-size: 12px;
                border: 1px solid #ccc;
                padding: 5px 10px;
                cursor: pointer;
                &.cur {
                    border-bottom: 2px solid blue;
                    background: rgb(0, 0, 255);
                    color: white;
                    font-family: serif;
                }
            }
        }
        .bd {
            height: 140px;
            .contentRow {
                font-family: 'consolas';
                line-height: 25px;
                a {
                    display: inline-block;
                    padding-left: 6px;
                }
            }
            .p_box {
                height: 130px;
                overflow: auto;
            }
        }
    }
</style>