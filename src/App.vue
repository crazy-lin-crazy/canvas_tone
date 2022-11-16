<template>
    <div id="app">
        <div class="canvas-container">
            <canvas id="canvas" ref="canvas">
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
        }
        return {data}
    },
    mounted(){
        let me = this
        // init

    },
    methods: {
        init(){

        },
        start(e){
            let me = this
            let data = me.data
            data.isDown = true;
            context.beginPath();
            data.canvasX = e.pageX - selectCanvas.offsetLeft;
            data.canvasY = e.pageY - selectCanvas.offsetTop;
            context.moveTo(canvasX, canvasY);
        },
        draw(e){
            let me = this
            let data = me.data
            if(data.isDown) {
                data.canvasX = e.pageX - selectCanvas.offsetLeft;
                data.canvasY = e.pageY - selectCanvas.offsetTop;
                context.lineTo(data.canvasX, data.canvasY);
                context.strokeStyle = selectedColor.value;
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
