<template>
  <div class="content">
    <div class="progress">
      <div class="progress__outer" :style="{ height: stroke_width + 'px'}">
        <div class="progress__inner" :style="barStyle">
             <div class="progress--innerText" v-if="textInside && showtext">{{ percentage + '%'}}</div>
        <div v-else class="progress--text" :style="{ fontSize: progressTextSize + 'px'}">
          <template v-if="!status && showtext">{{ percentage + '%'}}</template>
          <i v-else class="iconfont" :class="iconClass"></i>
        </div>
        </div>
       
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    stroke_width: {
      type: Number,
      default: 6
    },
    percentage: {
      type: Number,
      required: true,
      default: 0,
      validator: value => value >= 0 && value <= 100
    },
    status: {
      type: String
    },
    type: {
      type: String,
      default: "line",
      validator: val => ["line", "circle"].includes(val)
    },
    textInside: {
      type: Boolean,
      default: false
    },
    showtext:{
        type:Boolean,
        default:true
    },color:{
        type:String
    }
  },
  data() {
    return {};
  },
  computed: {
    progressTextSize() {
      return 12 + this.stroke_width * 0.4;
    },
    stroke() {
      let color;
      if(this.color){
          return this.color;
      }
      switch (this.status) {
        case "success":
          color = "#13ce66";
          break;
        case "exception":
          color = "#ff4949";
          break;
        default:
          color = "#20a0ff";
      }
      return color;
    },
    barStyle() {
      return { width: this.percentage + "%", background: this.stroke };
    },
    iconClass() {
      if (this.type === "line") {
        return this.status === "success"
          ? "iconfont-cicel-close"
          : "iconfont-cicel-check";
      } else {
        return this.status === "success"
          ? "iconfont-cicel-close"
          : "iconfont-cicel-check";
      }
    }
  }
};
</script>
<style>
@font-face {
  font-family: "iconfont"; /* project id 1407608 */
  src: url("//at.alicdn.com/t/font_1407608_9e1wd7x7ag.eot");
  src: url("//at.alicdn.com/t/font_1407608_9e1wd7x7ag.eot?#iefix")
      format("embedded-opentype"),
    url("//at.alicdn.com/t/font_1407608_9e1wd7x7ag.woff2") format("woff2"),
    url("//at.alicdn.com/t/font_1407608_9e1wd7x7ag.woff") format("woff"),
    url("//at.alicdn.com/t/font_1407608_9e1wd7x7ag.ttf") format("truetype"),
    url("//at.alicdn.com/t/font_1407608_9e1wd7x7ag.svg#iconfont") format("svg");
}
.iconfont {
  font-family: "iconfont" !important;
  font-size: 25px;
  font-style: normal;
}
.iconfont-cicel-check::before {
  content: "\e601";
  color: f56c6c;
}
.iconfont-cicel-close::before {
  content: "\e600";
  color: #67c23a;
}
* {
  margin: 0px;
  padding: 0px;
}
.content {
  position: relative;
}
.progress {
  width: 97.5%;
  display: inline-block;
  box-sizing: border-box;

}
.progress__outer {
  width: 100%;
  margin-top: 30px;
  background: #ccc;
  border-radius: 100px;
}
.progress__inner {
  height: 100%;
  margin-top: -0.5%;
  border-radius: 100px;
  transition: width 0.5s ease;
  text-align: right;
  line-height: 1;
  vertical-align: middle;
}
.progress--innerText {
  color: #fff;
  /* position: absolute;
    top: 55%; */ 
    margin: 5px 5px;
}
.progress--text {
  position: absolute;
  right: 0%;
  top: 55%;
  display: inline-block;
  color: #606266;
}
</style>
