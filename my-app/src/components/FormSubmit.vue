<template>

    <section>
        <h1>同学录</h1>

        <el-row :offset="1">
            <el-col id="main">
                <div class="groupForm">
                    <label>姓名：</label>
                    <el-input v-model="user.name" placeholder="请输入姓名"></el-input>
                </div>

                <div class="groupForm">
                    <label>性别：</label>
                    <el-select v-model="user.sex" placeholder="请选择">
                        <el-option v-for="item in options" :key="item" :value="item"></el-option>
                    </el-select>
                </div>

                <div class="groupForm">
                    <label>电话号码：</label>
                    <el-input v-model="user.phone" placeholder="请输入电话号码"></el-input>
                </div>

                <div class="groupForm">
                    <label>出生日期：</label>
                    <el-date-picker v-model="user.birth" format="yyyy 年 MM 月 dd 日" value-format="yyyy-MM-dd"
                                    align="right"
                                    type="date"
                                    placeholder="选择日期">
                    </el-date-picker>
                </div>
                <div>
                    <el-button type="primary" @click="submitForm()">新增</el-button>
                </div>
            </el-col>
        </el-row>


        <el-col class="toolbar">
            <el-form :inline="true">
                <el-form-item>
                    <el-input placeholder="请输入姓名" v-model="selectName"></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" icon="el-icon-search" @click="getUsers">查询</el-button>
                </el-form-item>
            </el-form>
        </el-col>

        <el-table align="left" :data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))">
            <el-table-column prop="name" label="姓名"></el-table-column>
            <el-table-column prop="phone" label="电话号码："></el-table-column>
            <el-table-column label="操作">
                <template slot-scope="scope">
                    <el-button type="primary" icon="el-icon-edit" circle @click="editUser"></el-button>
                    <el-button type="danger" icon="el-icon-delete" circle
                               @click="delUser(scope.$index)"></el-button>
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
                currentIndex     : 0,
                search:'',
                selectName:'',
                user          : {
                    name  : '',
                    sex   : '',
                    phone : '',
                    birth : ''

                },
                tableData     : [
                    {
                        id    : 1,
                        name  : '风月',
                        sex   : '女',
                        phone : '12223',
                        birth : '2019-10-12'
                    },
                    {
                        id    : 2,
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
        created: function () {
            this.currentIndex = this.tableData.length;
        },
        methods : {
            submitForm(){
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
                this.user.id = this.currentIndex++;
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
            getUsers(){alert(this.selectName);
                this.search = this.selectName;
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

<style lang="scss" itemscope="">
    section{
        background: #FFffff;
        padding: 30px 10px;
        margin: 30px auto;
    }
    #main {
        float: none;
        margin: 0 auto;
    }

    .groupForm{
        display: flex;
        justify-content: flex-start;
        align-items: baseline;
        margin-bottom: 10px;
    }
    .groupForm label {
        min-width: 80px;
        overflow: hidden;
        display: inline-block;
        text-align: right;
    }
    .groupForm button{
        align-self: center;
    }


    .toolbar form {
        border-top:1px solid #f2f2f2;
        padding-top: 30px;
        margin-top: 30px;
        display: flex;
        justify-content: flex-start;
        align-items: baseline;
    }

</style>
