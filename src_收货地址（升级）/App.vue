<template>
    <div>
        <Layout>
            <Header>
                <Menu mode="horizontal" theme="dark" active-name="1">
                    <div class="layout-logo">
                        牙牙乐网店管理系统
                    </div>
                    <div class="layout-nav">
                        <MenuItem name="1">
                        <Icon type="ios-navigate"></Icon>
                        网店
                        </MenuItem>
                        <MenuItem name="2">
                        <Icon type="ios-keypad"></Icon>
                        管理
                        </MenuItem>
                        <MenuItem name="3">
                        <Icon type="ios-analytics"></Icon>
                        用户
                        </MenuItem>
                        <MenuItem name="4">
                        <Icon type="ios-paper"></Icon>
                        管理
                        </MenuItem>
                    </div>
                </Menu>
            </Header>
            <Layout>
                <Sider hide-trigger :style="{background: '#fff'}">
                    <Menu active-name="1-2" theme="light" width="auto" :open-names="['1']">
                        <Submenu name="1">
                            <div slot="title">
                                <Icon type="ios-navigate"></Icon>
                               管理设置
                            </div>
                            <MenuItem name="1-1">历史订单管理</MenuItem>
                            <MenuItem name="1-2">收货地址管理</MenuItem>
                            <MenuItem name="1-3">历史退货管理</MenuItem>
                        </Submenu>
                        <Submenu name="2">
                            <div slot="title">
                                <Icon type="ios-keypad"></Icon>
                               收货地址管理
                            </div>
                            <MenuItem name="2-1">Option 1</MenuItem>
                            <MenuItem name="2-2">Option 2</MenuItem>
                        </Submenu>
                        <Submenu name="3">
                            <div slot="title">
                                <Icon type="ios-analytics"></Icon>
                                历史退货管理
                            </div>
                            <MenuItem name="3-1">Option 1</MenuItem>
                            <MenuItem name="3-2">Option 2</MenuItem>
                        </Submenu>
                    </Menu>
                </Sider>
                <Layout :style="{padding: '0 24px 24px'}">
                    <Breadcrumb :style="{margin: '24px 0'}">
                        <BreadcrumbItem>Home</BreadcrumbItem>
                        <BreadcrumbItem>Components</BreadcrumbItem>
                        <BreadcrumbItem>Layout</BreadcrumbItem>
                    </Breadcrumb>
                    <Content :style="{padding: '24px', minHeight: '280px', background: '#fff'}">
                        <Shdzgl />
                    </Content>
                </Layout>
            </Layout>
        </Layout>
    </div>
</template>

<script>
    import Shdzgl from './Shdzgl.vue'
    export default {
        components: {
            Shdzgl
        }
    }
</script>

<style lang="less" scoped>
    .layout {
        border: 1px solid #d7dde4;
        background: #f5f7f9;
        position: relative;
        border-radius: 4px;
        overflow: hidden;
    }
    .layout-logo {
        width: 135px;
        height: 30px;
        background: #5b6270;
        border-radius: 3px;
        float: left;
        position: relative;
        top: 15px;
        left: 20px;
        color: white;
        font-size: 15px;
        text-align: center;
        line-height: 30px;
    }
    .layout-nav {
        width: 420px;
        margin: 0 auto;
        margin-right: 20px;
    }
</style>