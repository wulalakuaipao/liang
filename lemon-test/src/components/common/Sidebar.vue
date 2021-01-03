<template>
    <div class="sidebar">
        <!--<el-menu class="sidebar-el-menu" :default-active="onRoutes" :collapse="collapse" unique-opened router>-->

        <el-menu class="sidebar-el-menu" :default-active="onRoutes" :collapse="collapse" background-color="#324157"
                 text-color="#bfcbd9" active-text-color="#20a0ff" unique-opened router>
            <template v-for="item in items">
                <template v-if="item.subs">
                    <el-submenu :index="item.index" :key="item.index">
                        <template slot="title">
                            <i :class="item.icon"></i><span slot="title">{{ item.title }}</span>
                        </template>
                        <template v-for="subItem in item.subs">
                            <el-submenu v-if="subItem.subs" :index="subItem.index" :key="subItem.index">
                                <template slot="title">{{ subItem.title }}</template>
                                <el-menu-item v-for="(threeItem,i) in subItem.subs" :key="i" :index="threeItem.index">
                                    {{ threeItem.title }}
                                </el-menu-item>
                            </el-submenu>
                            <el-menu-item v-else :index="subItem.index" :key="subItem.index">
                                {{ subItem.title }}
                            </el-menu-item>
                        </template>
                    </el-submenu>
                </template>
                <template v-else>
                    <el-menu-item :index="item.index" :key="item.index">
                        <i :class="item.icon"></i><span slot="title">{{ item.title }}</span>
                    </el-menu-item>
                </template>
            </template>
        </el-menu>
    </div>
</template>

<script>
    import bus from '../common/bus';
    export default {
        data() {
            return {
                collapse: false,
                items: [
                    {
                        icon: 'el-icon-s-home',
                        index: 'dashboard',
                        title: '系统首页'
                    },
                    {
                        icon: 'el-icon-s-claim',
                        index: '1',
                        title: '项目管理',
                        subs: [
                            {
                                index: 'projects_list',
                                title: '项目列表'
                            },
                            {
                                index: 'projects_add',
                                title: '项目新增'
                            }
                        ]
                    },
                    {
                        icon: 'el-icon-s-open',
                        index: '2',
                        title: '环境管理',
                        subs: [
                            {
                                index: 'envs_list',
                                title: '环境列表'
                            },
                            {
                                index: 'envs_add',
                                title: '环境新增'
                            }
                        ]
                    },
                    {
                        icon: 'el-icon-s-tools',
                        index: '3',
                        title: '内置函数',
                        subs: [
                            {
                                index: 'builtin_list',
                                title: '函数列表'
                            },
                            // {
                            //     index: 'builtin_edit',
                            //     title: '函数编辑'
                            // }
                        ]
                    },
                    {
                        icon: 'el-icon-s-flag',
                        index: '4',
                        title: '接口管理',
                        subs: [
                            {
                                index: 'interfaces_list',
                                title: '接口列表'
                            },
                            {
                                index: 'interfaces_add',
                                title: '接口新增'
                            }
                        ]
                    },
                    {
                        icon: 'el-icon-s-opportunity',
                        index: '8',
                        title: '用例管理',
                        subs: [
                            {
                                index: 'testcases_list',
                                title: '用例列表'
                            },
                            {
                                index: 'testcases_add',
                                title: '用例新增'
                            }
                        ]
                    },
                    {
                        icon: 'el-icon-s-ticket',
                        index: '10',
                        title: '配置管理',
                        subs: [
                            {
                                index: 'configures_list',
                                title: '配置列表'
                            },
                            {
                                index: 'configures_add',
                                title: '配置新增'
                            }
                        ]
                    },
                    {
                        icon: 'el-icon-files',
                        index: '13',
                        title: '套件管理',
                        subs: [
                            {
                                index: 'testsuites_list',
                                title: '套件列表'
                            },
                            {
                                index: 'testsuites_add',
                                title: '套件新增'
                            }
                        ]
                    },
                    {
                        icon: 'el-icon-s-marketing',
                        index: '16',
                        title: '报告管理',
                        subs: [
                            {
                                index: 'reports_list',
                                title: '报告列表'
                            }
                        ]
                    }
                ]
            }
        },
        computed:{
            onRoutes(){
                // return this.$route.path.replace('/','');
                return this.$route.path;

            }
        },
        created(){
            // 通过 Event Bus 进行组件间通信，来折叠侧边栏
            bus.$on('collapse', msg => {
                this.collapse = msg;
            })
        }
    }
</script>

<style scoped>
    .sidebar{
        display: block;
        position: absolute;
        left: 0;
        top: 70px;
        bottom:0;
        overflow-y: scroll;
    }
    .sidebar::-webkit-scrollbar{
        width: 0;
    }
    .sidebar-el-menu:not(.el-menu--collapse){
        width: 250px;
    }
    .sidebar > ul {
        height:100%;
    }
</style>
