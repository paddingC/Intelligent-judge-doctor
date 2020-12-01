<template>
    <div class="chronicDisease">
        <div class="div1">
            <div class="video">
                1
            </div>
            <div class="patient-info">
                <h3 class="border-left"> 患者信息</h3>
                <p><span>患者姓名</span>: <span>的点点滴滴多多</span></p>
                <p><span>性别</span>: <span>的点点滴滴多多</span></p>
                <p><span>年龄</span>: <span>的点点滴滴多多</span></p>
                <p><span>联系电话</span>: <span>的点点滴滴多多</span></p>
            </div>
        </div>
        <div class="div2">
            <div class="recipel-info">
                <h3 class="border-left"> 处方基本信息</h3>
                <p><span>处方类型</span>: <span>的点点滴滴多多</span></p>
                <p><span>处方单号</span>: <span>的点点滴滴多多</span></p>
                <p><span>开方时间</span>: <span><el-date-picker
                    v-model="form.value1"
                    type="date"
                    placeholder="选择日期">
    </el-date-picker></span></p>
            </div>
            <div class="recipel-picture">
                <h3 class="border-left"> 处方信息</h3>
                <el-image
                    style="width: 100%; height:100%"
                    :src="srcList[0]"
                    :preview-src-list="srcList">
                </el-image>
            </div>
        </div>
        <div class="div3">
            <h3 class="border-left">审方信息</h3>
            <p><span>处方单</span>: <span>普通处方||特药处方</span></p>
            <p><span>是否有过敏史</span>: <span>  <el-radio v-model="form.radio2" label="1">有</el-radio>
  <el-radio v-model="form.radio2" label="2">无</el-radio></span></p>
            <p><span>审核意见</span>: <span>  <el-radio v-model="form.radio" label="1">审核通过</el-radio>
  <el-radio v-model="form.radio" label="2">审核不通过</el-radio></span></p>
            <div>
                <h3 style="line-height: 40px;">审核不通过原因 :</h3>
                <br>
                <el-input
                    type="textarea"
                    :disabled="disabled"
                    :autosize="{ minRows: 2, maxRows: 4}"
                    placeholder="审核不通过原因"
                    v-model="form.textarea">
                </el-input>
            </div>
            <p style="margin: 50px 0 0 20px">
                <el-button class="search" @click="submit">提交</el-button>
            </p>
        </div>
        <el-dialog title="指纹注册与校验" :visible.sync="outerVisible">
            <el-dialog
                width="30%"
                title="提示"
                :visible.sync="innerVisible"
                append-to-body
                :before-close="handleClose"
            >
                <p>将手指放到指纹仪上,并点击确定</p>
                <div slot="footer" class="dialog-footer">
                    <el-button @click="innerVisibleCancel">取 消</el-button>
                    <el-button type="primary" :loading="loading" @click="innerVisibleClick">确定</el-button>
                </div>
            </el-dialog>
            <div class="main-content">
                <div class="img">
                    <h3 class="border-left">图像采集区域</h3>
                    <div class="img-box">
                        <span>1</span>
                    </div>
                </div>
                <div class="info">
                    <h3 class="border-left">提示信息</h3>
                    <div class="info-box">
                        <span>
                            提示 :
                        </span>
                    </div>
                </div>
            </div>
            <div slot="footer" class="dialog-footer">
                <el-button @click="outerVisible = false">取 消</el-button>
                <el-button type="primary" @click="outerVisible = false">确定</el-button>
            </div>
        </el-dialog>
    </div>
</template>

<script>
export default {
    name: "ordinarySpecial",
    data() {
        return {
            disabled: true,
            form: {
                value1: '2012-08-01',
                input: '',
                textarea: '',
                radio: '1',
                radio2: '2',
            },
            outerVisible: false,
            innerVisible: false,
            srcList: [
                'https://fuss10.elemecdn.com/8/27/f01c15bb73e1ef3793e64e6b7bbccjpeg.jpeg',
                'https://fuss10.elemecdn.com/1/8e/aeffeb4de74e2fde4bd74fc7b4486jpeg.jpeg'
            ],

            loading: false
        }
    },
    methods: {
        innerVisibleCancel() {
            // this.outerVisible = false
            // this.innerVisible = false
        },
        innerVisibleClick() {
            console.log(111)
            this.loading = true
            setTimeout(() => {
                this.loading = false
                this.innerVisible = false
            }, 2000)
        },
        open() {
            this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
                confirmButtonText: '确定',
                cancelButtonText: '取消',
                type: 'warning'
            }).then(() => {
                this.$message({
                    type: 'success',
                    message: '删除成功!'
                })
            }).catch(() => {
                this.$message({
                    type: 'info',
                    message: '已取消删除'
                })
            })
        },
        handleClose(done) {
            // console.log(111)
            // this.loading = true
            // setTimeout(() => {
            //     this.loading=false
            //     done()
            // },2000)
            this.$confirm('确认关闭？')
                .then(_ => {
                    done()
                })
                .catch(_ => {})
        },
        submit() {
            if (this.form.radio === '2' && !this.form.textarea) {
                this.$message.warning("请在填写诊断病症和开放时间后提交")
                return false
            } else {
                this.outerVisible = true
                this.$nextTick(() => {
                    this.innerVisible = true
                })
            }
        }
    },
    watch: {
        "form.radio": {
            deep: true,
            handler(val) {
                console.log(val)
                if (val === '2') {
                    this.disabled = false
                } else {
                    this.disabled = true
                    this.form.textarea = ''
                }
            }
        }
    }
}
</script>

<style scoped lang="scss">
    .chronicDisease {
        .search {
            color: #FFF;
            background-color: $color-btn;
            border-color: $color-btn;
        }

        height: 100%;
        width: 100%;
        bottom: 0px;
        display: -webkit-box;
        display: flex;
        display: -ms-flex;
        display: -webkit-flex;
        font-size: 18px;

        .div1, .div2, .div3 {
            padding: 5px;

            flex: 1;
            -ms-flex: 1;
            -webkit-flex: 1;
            -webkit-box-flex: 1;
            position: relative;
            height: 100%;

            .border-left {
                line-height: 30px;
                border-left: 3px solid #36C2AA;
                font-size: 22px;
                margin: 10px 0;
                padding-left: 15px;
            }
        }

        .div1 {
            .video {
                height: 50%;
                background-color: lightblue;
            }

            .patient-info {
                height: 50%;


                p {
                    line-height: 40px;
                    font-size: 16px;

                    & span:first-child {
                        display: inline-block;
                        text-align-last: justify;
                        text-align: justify;
                        text-justify: distribute-all-lines; // 这行必加，兼容ie浏览器
                        width: 80px;
                    }

                    & span:last-child {
                        display: inline-block;
                        padding: 0 10px;
                        color: #909399;
                    }
                }
            }
        }

        .div2 {

            .recipel-info {
                height: 50%;

                h3 {
                    line-height: 30px;
                    border-left: 3px solid #36C2AA;
                    font-size: 22px;
                    margin: 10px 0;
                    padding-left: 15px;
                }

                p {
                    line-height: 40px;
                    font-size: 16px;

                    & span:first-child {
                        display: inline-block;
                        text-align-last: justify;
                        text-align: justify;
                        text-justify: distribute-all-lines; // 这行必加，兼容ie浏览器
                        width: 80px;
                    }

                    & span:last-child {
                        display: inline-block;
                        padding: 0 10px;
                        color: #909399;
                    }
                }
            }

            .recipel-picture {
                height: 50%;
            }
        }

        .div3 {
            p {
                line-height: 40px;
                font-size: 16px;

                & span:first-child {
                    display: inline-block;
                    text-align-last: justify;
                    text-align: justify;
                    text-justify: distribute-all-lines; // 这行必加，兼容ie浏览器
                    width: 100px;
                }

                & span:last-child {
                    display: inline-block;
                    padding: 0 10px;
                    color: #909399;
                }
            }
        }

        /deep/ .el-dialog__body {
            padding: 15px 15px;
        }

        .main-content {
            height: 500px;
            display: flex;
            flex-direction: column;

            .border-left {
                line-height: 25px;
                border-left: 3px solid #36C2AA;
                font-size: 22px;
                margin: 5px 0;
                padding-left: 15px;
            }

            .img {
                flex: 1;

                .img-box {
                    height: calc(100% - 35px);
                }
            }

            .info {
                height: 200px;

                .info-box {
                    height: calc(100% - 35px);
                    padding: 10px;
                }
            }
        }

    }
</style>
