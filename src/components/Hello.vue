<template>
<div class="kp">{{hoursTip}},欢迎使用此系统</div>
</template>

<script>
export default {
    data() {
        return {
            hoursTip: '',
        }
    },
    created() {
        this.getMycount();
    },
    methods: {
        getMycount() {
            let self = this;
            let date = new Date();

            if (date.getHours() >= 0 && date.getHours() < 12) {

                self.hoursTip = "上午好"

            } else if (date.getHours() >= 12 && date.getHours() < 18) {

                self.hoursTip = "下午好"

            } else {

                self.hoursTip = "晚上好"

            }
        }
    }

}
</script>

<style lang="less" scoped>
.kp {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 5rem;
}
</style>
