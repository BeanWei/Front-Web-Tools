<template>
  <div id="test">
    <div style="width:100%; height:1000px; background-color:#F2F2F2;"></div>
    <div class="bottomHalf" 
        :style="{height: bottomHalfHeight + 'px'}" 
        @mousedown = dragPanel($event)>
        <div id="expander"></div><span id="info">这里是内容区</span>
    </div>
  </div>
</template>

<script>
export default {
    data: function() {
        return {
            src_posi_Y: 0, 
            dest_posi_Y: 0, 
            move_Y: 0, 
            is_mouse_down: false, 
            destHeight: 30,
            bottomHalfHeight: 30
        }
    },
    watch: {
        'bottomHalfHeight': {
            handler(newVal){
                this.bottomHalfHeight = newVal
                console.log("监听成功: ", this.bottomHalfHeight)
            }
        } 
    },
    methods: {
        dragPanel(ev) {
            let that = this;
            document.onmousedown = function(e) {
                console.log("鼠标按下")
                that.src_posi_Y = e.pageY;
                that.is_mouse_down = true
            };
            document.onmouseup = function(e) {
                console.log("鼠标抬起")
                if (that.is_mouse_down) {
                    that.is_mouse_down = false
                }
            };
            document.onmousemove = function(e){
                console.log("鼠标移动")
                that.dest_posi_Y = e.pageY;
                that.move_Y = that.src_posi_Y - that.dest_posi_Y
                that.src_posi_Y = that.dest_posi_Y
                that.destHeight = that.bottomHalfHeight + that.move_Y
                if (that.is_mouse_down) {
                    if (that.destHeight < 30 ) {
                        that.destHeight = 30
                    }
                    that.bottomHalfHeight = that.destHeight
                }
            };
            this.bottomHalfHeight = that.bottomHalfHeight
        }
    }
}
</script>

<style>
.bottomHalf {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    background-color: #B8D0FA;
}

#expander {
    width: 100%;
    height: 6px;
    background-color: rgb(252, 115, 115);
}

#expander:hover {
    cursor: n-resize;
}
</style>