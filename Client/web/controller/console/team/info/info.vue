<template>
    <el-row class="row" style="margin-top: 10px;font-size: 14px" id="teamInfo">
        <el-tabs v-model="type" style="height: 50px;">
            <el-tab-pane :name="0" label="概况">
                <teaminfo></teaminfo>
            </el-tab-pane>
            <el-tab-pane :name="1" label="成员">
                <teamuser></teamuser>
            </el-tab-pane>
        </el-tabs>
    </el-row>
</template>

<style>
    #teamInfo .el-tabs__header {
        background-color: white;
    }
    #teamInfo .el-tabs__nav-scroll {
        padding-left: 20px;
        padding-right: 20px;
    }
    #teamInfo .el-tabs__header {
        margin-bottom: 5px;
    }
</style>

<script>
    var teamInfo=require("./component/teamInfo.vue");
    var teamUser=require("./component/teamUser.vue");
    var store=require("../../store")._modulesNamespaceMap["team/info/"].context;
    var sessionChange=require("common/mixins/session");
    var refresh=require("common/mixins/refresh");
    module.exports = {
        data: function () {
            return {
                type:0
            }
        },
        mixins:[sessionChange,refresh],
        store:store,
        components:{
            "teaminfo":teamInfo,
            "teamuser":teamUser

        },
        methods: {},
        created:function () {
            var _this=this;
            this.$store.getters.event.$on("updateTeamProjectList",function (list) {
                _this.$store.state.project=list;
            })
        },
        mounted:function () {
            this.$nextTick(function () {
                Vue.prototype.$message("团队的项目列表移动到左侧的项目标签页了！")
            })
        }
    }
</script>