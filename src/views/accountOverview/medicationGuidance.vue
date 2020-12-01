<template>
    <div class="medicationGuidance">
        <section class="video">
            <!--            <el-card shadow="always" style="height: 100%;width: 100%">-->
            <el-image :fit="fit" src="https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg"
                      lazy></el-image>
            <!--            </el-card>-->
        </section>
        <section class="button-end">
            <el-button @click="endGuidance">结束指导</el-button>
        </section>
    </div>
</template>

<script>
export default {
    name: "medicationGuidance",
    data() {
        return {
            fit: 'cover'
        }

    },
    methods: {
        endGuidance() {
            this.$message("结束指导")
        }
    },
    created() {

        this.$store.commit('app/SET_ROUTER', '/home/accountOverview/information')
    }
}
</script>

<style lang="scss" scoped>
    .medicationGuidance {
        padding: 40px;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;

        .video {
            width: 90%;
            flex: 1;
            overflow: hidden;
            box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);

            & /deep/ .el-image {
                width: 100%;
                height: 100%;
            }

            img {
                width: 100%;
                height: 100%;
            }
        }

        .button-end {
            height: 100px;
            line-height: 100px;
        }
    }
</style>
