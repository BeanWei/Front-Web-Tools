<template>
    <div id="windowtest">
        <div class="sub"></div>
        <div class="sub" v-if="show"></div>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            //监听高度
            theInitHeight: 0,
            show: true,
        }
    },
    mounted() {
        this.theInitHeight = parseInt(document.documentElement.clientHeight);
        const that = this;
        window.onresize = function windowResize() {
            var theHeight = parseInt(document.documentElement.clientHeight);
            if ((that.theInitHeight - theHeight) > that.theInitHeight/16) {
                that.show = false;
            } else {
                that.show = true;
            }
        }
    },
}
</script>

<style scoped>
.sub {
    width: 100%;
    height: 50%;
}
</style>
