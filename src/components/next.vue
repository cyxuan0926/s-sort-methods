<template>
  <div class="container">
    <h1>S型排序</h1>

    <input type="number" placeholder="请输入每行数量" v-model.number="num" min="0">

    <input type="number" placeholder="请输入总数" v-model.number="total" min="0">

    <div class="flex-box" :style="flexBoxStyle">
      <template v-for="item in total">
        <span :key="item" :style="{
          flex: ` 0 0 ${ ( 1/num - 0.01) * 100 }% `,
          borderTop: item > num ? 'none' : '1px solid red',
          order: isWhichRows(item) % 2 === 0 ? countIndex(item) : item,
          borderLeft:
            isWhichRows(item) === 1
            ? ''
            :
              (isWhichRows(item) % 2 === 0
                ? (rowMax(item) === item  ? '1px solid red' : '')
                : ((isWhichRows(item) - 1)* num + 1 === item ? '1px solid red' : ''))
        }">{{ item }}</span>
      </template>
    </div>
  </div>
</template>

<script>
// 23个 3行
export default {
  data () {
    return {
      num: 0,
      total: 0
    }
  },

  computed: {
    // 1, 2, 3, 4, 5
    // 5, 4, 3, 2, 1
    // 每一行都是公差为1的等差数列
    // 奇数/偶数flex-box的样式
    flexBoxStyle () {
      return this.count % 2 === 0 ? ({ justifyContent: 'flex-end' }) : ({})
    },

    // 行数
    count () {
      let result
      if (this.num && this.total) result = Math.ceil(this.total / this.num)
      else result = 0
      return result
    },

    // 最后一行的数目
    // 如果为 0 就是满行数
    endRowCounts () {
      return this.total % this.num
    }
  },

  methods: {
    // 偶数行 反向排列
    isWhichRows (index) {
      return (Math.ceil(index / this.num))
    },

    // 某一行的最大值
    rowMax (index) {
      const row = this.isWhichRows(index)
      let num = row === this.count && this.endRowCounts ? this.endRowCounts : this.num
      return (row - 1) * this.num + num
    },

    // 偶数行 某一个数实际对应的数
    countIndex (index) {
      let num = this.num
      const row = this.isWhichRows(index)
      // 说明是偶数行并且是最后一行 并且不是整数
      const min = (row - 1) * this.num + 1
      if (row === this.count && this.endRowCounts) {
        num = this.endRowCounts
      }
      const max = min + num - 1
      const nowIndex = max - index
      const result = min + nowIndex
      return result
    }
  }
}
</script>

<style scoped>
.flex-box {
  margin-top: 20px;
  width: 80%;
  /* height: 300px; */
  display: flex;
  flex-wrap: wrap;
  /* justify-content: flex-end; */
}
span {
 border: 1px solid red;
}
span + span {
  border-left: none;
}
</style>
