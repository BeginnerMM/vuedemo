<template>
    <div>
        <h2 style="margin-top:20px;">线性进度条-----外显</h2>
        <d-progress :percentage='30' status='success'></d-progress>
        <d-progress :percentage='30'/>
       <d-progress :percentage='50'  />
       <d-progress color="orange" :percentage='70' />
       <d-progress :percentage='60' status="exception"/>
       <d-progress :percentage='90' status="success"/>
       <br>
       <h2 style="margin-top:20px;">线性进度条-----内显</h2>
       <d-progress :percentage='70' :stroke_width="18" status="exception" :textInside="true"></d-progress>   
        <d-progress color="pink" :percentage='60' :stroke_width="18"  :textInside="true"></d-progress>
         <d-progress :percentage='30' :stroke_width="18" status="success"  :textInside="true"></d-progress>
          <d-progress :percentage='90' :stroke_width="18"  :textInside="true"></d-progress>
    </div>
</template>
<script>
import DProgress from './Progress';

export default {
    components:{
        DProgress,
    },
    data(){
        return { 
        }
    }
}
</script>
<style>
    
</style>