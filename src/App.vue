<template>
    <div id="app">
        <div class="canvas-container">
            <canvas id="canvas" ref="canvas" @mousedown="start" @mouseup="stop" @mousemove="draw">
                Oops! Canvas not supported in this browser
            </canvas>
        </div>
    </div>
</template>

<script>

export default {
    name: 'App',
    data(){
        let data = {
            isDown:false,
            canvasX:0,
            canvasY:0,
            canvasEL:{},
        }
        return {data}
    },
    mounted(){
        let me = this
        // init
        me.data.canvasEL = me.$refs.canvas
    },
    methods: {
        init(){

        },
        start(e){
            let me = this
            let data = me.data
            data.isDown = true;
            context.beginPath();
            data.canvasX = e.pageX - data.canvasEL.offsetLeft;
            data.canvasY = e.pageY - data.canvasEL.offsetTop;
            context.moveTo(data.canvasX, data.canvasY);
        },
        draw(e){
            let me = this
            let data = me.data
            if(data.isDown) {
                data.canvasX = e.pageX - data.canvasEL.offsetLeft;
                data.canvasY = e.pageY - data.canvasEL.offsetTop;
                context.lineTo(data.canvasX, data.canvasY);
                context.strokeStyle = '#000';
                context.stroke();
            }
        },
        stop(e){
            let me = this
            let data = me.data
            data.isDown = false;
            context.closePath();
        },
        changeStroke(e,obj){
            let me = this
            let data = me.data
            if(e.target.dataset.stroke){
                let parent = e.target.parentElement.children;
                for(let i in parent){
                    if(parent.hasOwnProperty(i)){
                        if(e.target.className === parent[i].className){
                            e.target.style.border = "2px dotted";
                        }else{
                            parent[i].style.border = "none";
                        }
                    }
                }
                context.lineWidth = e.target.dataset.stroke;
            }
        }
    }
}
</script>

<style lang="less">
#canvas{
    width:400px;
    height: 400px;
}

</style>
