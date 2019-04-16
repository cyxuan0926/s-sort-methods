<template>
  <div class="hello">
    <!-- <a :[attr]="url">Go to baidu</a> -->
    <h1>S型排序</h1>
    <input type="number" placeholder="请输入每行数量" v-model.number="num" min="0">
    <input type="number" placeholder="请输入总数" v-model.number="total" min="0">
    <div
      class="flex-box"
      v-for="(value, index) of val"
      :class="{'flex-reverser': index%2}"
      :key="value">
      <span
        v-for="index of num*value"
        v-show="index > num*(value-1) && index <= total"
        :key="index"
        :style="{flex: `0 1 ${(1/num-0.009)*100}%`}">
        {{index}}
      </span>
      <!-- <span class="item1">1</span>
      <span class="item2">2</span>
      <span class="item3">3</span>
      <span class="item4">4</span>
      <span class="item5">5</span>
      <span class="item6">6</span>
      <span class="item7">7</span>
      <span class="item8">8</span> -->
    </div>
  </div>
</template>

<script>
// 形式 display:flex 行内元素:display:inline-flex
// 采用Flex布局的元素，简称为容器。它的所有子元素自动称为容器成员，称为 项目
// 水平的主轴 垂直的交叉轴 默认沿主轴排列，main size cross size 默认情况下，
// 项目都排在一条线 flex-wrap: wrap nowrap wrap-reverse
// 容器的属性 flex-direction决定主轴的方向 row row-reverse column column-reverse
// justify-conent 定义了项目在主轴上的对齐方式 flex-start flex-end center space-between space-around
// align-items(垂直对齐):flex-start flex-end center baseline streth
// align-content属性定义了多根轴线的对齐方式,如果只有一个轴线，不起作用 flex-start flex-end center space-between space-around streth
// items属性：order属性定义项目的排列顺序，数值越小 排列越靠前 默认是0
// flex-grow:定义了项目的放大比列，默认为0，则如果存在剩余空间，也不会放大(放大当然是空间有余的时候)
// flex-shrink:定义了项目的缩小比列，默认为1，即如果空间不足，该项目将缩小(缩小当然是空间不足的时候)
// flex-basis属性：定义在分配多余空间的之前，项目占据的主轴空间
// flex属性：是flex-grow flex-shrink flex-basis的简写 默认值是 0 1 auto
// 该属性有两个快捷值：auto(1,1,auto) none(0,0,auto)
// align-self属性允许单个项目有与其它项目不一样的对齐方式，可以覆盖align-items属性默认值是auto
// 表示继承父元素的align-items属性，如果没有父元素，则等同于stretch
// auto flex-start flex-end  center baseline stretch
export default {
  name: 'HelloWorld',
  data () {
    return {
      // url: 'http://wwww.baidu.com',
      // attr: 'href'
      num: '',
      total: ''
    }
  },
  computed: {
    val () {
      if (this.num && this.total) return Math.ceil(this.total / this.num)
      return 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
span {
  border: 1px solid red;
  /* margin-left: 2px; */
  margin-top: 2px;
  /* align-content: space-between; */
  /* height: 30px; */
}
/* ol {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
} */
a {
  color: #42b983;
}
.flex-reverser {
  flex-direction: row-reverse;
}
.flex-box {
  width: 220px;
  /* height: 100px; */
  display: flex;
  /* flex-flow: row nowrap; */
  /* align-content:space-around; */
  /* justify-content: flex-start; */
  /* align-items: baseline; */
  /* flex-direction: row;
  flex-wrap: wrap-reverse; */
}
.item1 {
  /* order: 0; */
  /* flex-basis:100px; */
  /* flex-grow: 4; */
  /* flex-shrink: 0; */
  /* flex-basis: 20%; */
}
.item2 {
  /* order: 1; */
  /* flex-grow: 1; */
  /* flex-basis: 20%; */
}
.item3 {
  /* order: 2; */
  /* flex-grow: 1; */
}
.item4 {
  /* order: 6; */
  /* flex-grow: 1; */
}
.item5 {
  /* order: 5; */
  /* flex-grow: 1; */
}
.item6 {
  /* order: 4; */
  /* flex-grow: 1; */
}
.item7 {
  /* order: 7; */
  /* flex-grow: 1; */
}
.item8 {
  /* order: 8; */
  /* flex-grow: 1; */
}
</style>
