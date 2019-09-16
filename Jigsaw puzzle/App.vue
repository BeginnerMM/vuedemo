<template>
    <div>
        <d-puzz v-bind="puzzleConfig[level]" @next="handlenext"></d-puzz>
    </div>
</template>
<script>
import DPuzz from './Puzz';
export default {
    components:{
        DPuzz
    },
    data() {
        return {
            level:0,
            puzzleConfig:[
                {row:3,col:3,img:'./img/first.jpg'},
                {row:4,col:4,img:'./img/second.jpg'},
                {row:5,col:5,img:'./img/third.jpg'},
                {row:8,col:8,img:'./img/four.jpg'}
            ]
        }
    },
    methods: {
        handlenext(){
            if(++ this.level ==this.puzzleConfig.length){
             const answert =   window.confirm("已经是最后一关了，要重新开始嘛？");
            }
            if(answert){
                this.level = 0;
            }
        }
    },
}
</script>
<style>
    
</style>