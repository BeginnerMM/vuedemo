<template>
    <div class="puzz" :style="{ width:width+'px',height:height+'px' }">
        <div class="puzz__block" 
        v-for="(item,index) in blockpoint" :key="item.id" 
        :style="{width:blockWidth+'px',
        height:blockHeight+'px',
        left:item.x + 'px',
        top:item.y + 'px',
        backgroundImage:`url(${ img })`,
        backgroundSize:width + 'px',
        backgroundPosition:`-${ beforepoint[index].x }px -${ beforepoint[index].y }px`,
        opacity: index === blockpoint.length - 1 && 0,}" 
        @click = 'handleclick'
        :ref="index === blockpoint.length - 1 ? 'empty':'block'"
        :data-bbeleft="beforepoint[index].x"
        :data-bbetop="beforepoint[index].y">
        </div>
    </div>
</template>
<script>
export default {
    props:{
        width:{
            type:Number,
            default:500
        },
        height:{
            type:Number,
            default:500
        },
        row:{
            type:Number,
            default:3
        },
        col:{
            type:Number,
            default:3
        },
        img:{
            type:String,
            required:true
        }
    },
    computed: {
        blockWidth:function(){
            return this.width/this.col;
        },
        blockHeight:function(){
            return this.height/this.row;
        },
        beforepoint (){
            const {row,col,blockWidth,blockHeight} = this;
            // console.log(row,col,blockWidth,blockHeight);
            let arr = [];
            for(let i = 0; i < row; i ++){
                for(let j = 0; j < col; j++){
                    arr.push({
                        x:j * blockWidth,
                        y:i * blockHeight,
                        id:new Date().getTime() + Math.random()*100
                    })
                }
            }
            return arr;
        },
        blockpoint (){
            const points = this.beforepoint;
            const newArr = [...points];
            let len = points.length;
            let lastele = points[len - 1];
            newArr.length = newArr.length - 1;
            newArr.sort(()=>{return Math.random() - 0.5});
            newArr.push(lastele);
            return newArr;
        }
    },
    methods:{
        handleclick(e){
            const blockdom = e.target;
            const emptydom = this.$refs.empty[0];
            const beforeleft = blockdom.style.left;
            const beforetop = blockdom.style.top;
            // if(!this.istrue(blockdom,emptydom)){
            //     return;
            // }
                blockdom.style.left =  emptydom.style.left;
                blockdom.style.top = emptydom.style.top;
                emptydom.style.left = beforeleft;
                emptydom.style.top = beforetop;
            const winflag = this.checkwin();
            console.log(winflag);
            if(winflag){
                this.wingame(emptydom);
            }
        },
         istrue(blockdom,emptydom){
            let flag = true;
            const left = blockdom.style.left;
            const top = blockdom.style.top;
            const eleft = emptydom.style.left;
            const etop = emptydom.style.top;
            const width = this.blockWidth;
            const height = this.blockHeight;
            const xdis = Math.floor(Math.abs(parseFloat(top) - parseFloat(etop)));
            const ydis = Math.floor(Math.abs(parseFloat(left) - parseFloat(eleft)));
            flag = (left===eleft && xdis===parseInt(width))||
            (top===etop&& ydis===parseInt(height))
            return flag;
        },
        checkwin(){
            const blockArr = this.$refs.block;
            return blockArr.every(dom=>{
                    const domleft = dom.style.left;
                    const domtop = dom.style.top;
                    const bbeleft = dom.dataset.bbeleft;
                    const bbetop = dom.dataset.bbetop;
                    const flag = parseInt(domleft) === parseInt(bbeleft) && 
                    parseInt(domtop) === parseInt(bbetop);
                    return flag;
            })
        },
        wingame(emptydom){
            setTimeout(()=>{
                emptydom.style.opacity = 1;
                alert('恭喜你,进入下一关！');
                 setTimeout(()=>{
                    this.gotonextleval();
            },300)
            },300)
        },
        gotonextleval(){
           const answerlog =  window.confirm('确定进入下一关？');
           if(answerlog){
               this.$emit('next');
           }
        }
    },
    data() {
        return {
            
        }
    },
}
</script>
<style>
    .puzz{
        position: relative;
        border: 2px solid #ccc;
    }
    .puzz__block{
        position: absolute;
        /* background: orange; */
        border:1px solid #fff;
        box-sizing: border-box;
        background-repeat: no-repeat;
        transition: all .4s;
    }
</style>