<template>

    <section>
        <h1>同学录</h1>

        <el-row :span="22" :offset="1">
            <el-col id="main">
                <label>姓名：</label>
                <el-input v-model="user.name" placeholder="请输入姓名"></el-input>
                <br>
                <label>性别：</label>
                <el-select v-model="user.sex" placeholder="请选择">
                    <el-option v-for="item in options" :key="item" :value="item"></el-option>
                </el-select>
                <br>
                <label>电话号码：</label>
                <el-input v-model="user.phone" placeholder="请输入电话号码"></el-input>
                <br>
                <label>出生日期：</label>
                <el-date-picker v-model="user.birth" format="yyyy 年 MM 月 dd 日" value-format="yyyy-MM-dd" align="right"
                                type="date"
                                placeholder="选择日期">
                </el-date-picker>

            </el-col>
        </el-row>


        <el-col :span="22" class="toolbar" style="padding-bottom: 0; text-align: left">
            <el-form :inline="true">
                <el-form-item>
                    <el-input placeholder="请输入姓名"></el-input>
                </el-form-item>
                <el-form-item>

                    <el-button type="primary" icon="el-icon-search" @click="getUsers">查询</el-button>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="create">新增</el-button>
                </el-form-item>
            </el-form>
        </el-col>

        <el-table :data="tableData" align="left">
            <el-table-column prop="name" label="姓名"></el-table-column>
            <el-table-column prop="sex" label="性别"></el-table-column>
            <el-table-column prop="phone" label="电话号码："></el-table-column>
            <el-table-column prop="birth" label="出生日期："></el-table-column>
            <el-table-column label="操作">
                <template slot-scope="scope">
                    <el-button type="primary" icon="el-icon-edit" circle @click="editUser"></el-button>
                    <el-button type="danger" icon="el-icon-delete" circle
                               @click="delUser(scope.$index,scope.row)"></el-button>
                </template>
            </el-table-column>
        </el-table>


    </section>


</template>

<script>
    export default {

        data(){
            return {
                dialogVisible : false,
                userIndex     : 0,
                user          : {
                    name  : '',
                    sex   : '',
                    phone : '',
                    birth : ''

                },
                tableData     : [
                    {
                        name  : '风月',
                        sex   : '女',
                        phone : '12223',
                        birth : '2019-10-12'
                    },
                    {
                        name  : '风月1',
                        sex   : '女',
                        phone : '12223',
                        birth : '2019-10-11'
                    }
                ],
                editObj       : {
                    name  : '',
                    sex   : '',
                    phone : '',
                    birth : ''
                },
                options       : [
                    '女', '男', '保密'
                ]

            }

        },
        methods : {
            create(){
                if (!this.user.name) {
                    this.$message({
                        message : '请输入姓名',
                        type    : 'warning'
                    })
                    return
                }
                if (!this.user.sex) {
                    this.$message({
                        message : '请输入性别',
                        type    : 'warning'
                    })
                    return
                }
                if (!this.user.phone) {
                    this.$message({
                        message : '请输入电话号码',
                        type    : 'warning'
                    })
                    return
                }
                if (!this.user.birth) {
                    this.$message({
                        message : '请选择生日',
                        type    : 'warning'
                    })
                    return
                }
                this.tableData.push(this.user)
                this.user = {
                    name  : '',
                    sex   : '',
                    phone : '',
                    birth : ''
                }
            },
            editUser() {

            },
            delUser(index) {
                this.tableData.splice(index, 1)
            },
            handleClose() {
                this.dialogVisible = false
            },
            confirm(){
                this.dialogVisible = false
                this.$message({
                    type    : 'success',
                    message : '修改成功!'
                })
            }
        }
    }
</script>

<style lang="scss">
    #main {
        float: none;
        margin: 0 auto;
    }

    .el-input {
        /* padding-bottom: 5px; */
        width: 40%;
    }

    .btn-auto {
        width: 100%;
        margin-top: 12px;
    }

</style>
