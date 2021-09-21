<!-- 排名或者进度条组件 -->
<template>
  <div id="ranking">
    <div v-for="(item, index) in rankingDataCard" :key="index" class="ranking">
      <div class="ranking-left">
        {{ item.name }}
      </div>
      <div class="ranking-out ranking-right">
        <div
          v-if="item.type"
          class="ranking-inner"
          ref="inner"
          :style="{
            width: `${item.value * 100}%`
          }"
        >
          {{ (item.value * 100).toFixed(2) }}%
        </div>
        <div
          v-else
          class="ranking-inner"
          ref="inner"
          :style="{
            width: `${(item.value / rankingDataCard[0].value) * 100}%`
          }"
        >
          {{ item.value }}万
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    rankingData: {
      type: Array,
      default() {
        return [
          {
            name: "默认的名称",
            value: "默认的数值",
            type: "有type默认百分比。没有type单位是万"
          }
        ]
      }
    }
  },
  data() {
    return {
      rankingDataCard: []
    }
  },
  mounted() {
    // 设置延时是为了获取dom元素以及渲染有动画的效果
    setTimeout(() => {
      this.getRandomColor()
    }, 500)
  },
  watch: {
    rankingData(val) {
      console.log("排行组件", this.rankingData)
      this.rankingDataCard = this.rankingData
      this.getRandomColor()
    }
  },
  methods: {
    //   保留两位小数
    toFixed(val) {
      if (!val) throw Error("没有数据")
      val = val * 100
      if (val.toString().indexOf(".") === -1) {
        return val + ".00"
      } else {
        const arr = val.toString().split(".")
        console.log("arr", arr)
        const firstStr = arr[0]
        const lastStr = arr[1]
        console.log("lastStr", lastStr)
        if (lastStr.length < 2) {
          return `${firstStr}.${lastStr}0`
        } else {
          return `${firstStr}.${Number(lastStr).toFixed(0)}`
        }
      }
    },
    // 随机颜色,当然也可以将这个函数放在Style中调用（解开注释的地方，将未注释的地方注释掉）
    getRandomColor() {
      // const color =
      //   "#" +
      //   Math.floor(Math.random() * 0xffffff)
      //     .toString(16)
      //     .padEnd(6, "0")
      // return color

      const inner = this.$refs.inner
      if (inner) {
        inner.forEach((v) => {
          v.style.backgroundColor =
            "#" +
            Math.floor(Math.random() * 0xffffff)
              .toString(16)
              .padEnd(6, "0")
        })
      }
    }
  },
}
</script>

<style scoped lang="scss">
#ranking {
  .ranking {
    margin: 0.3rem 0;
    width: 94%;
    display: flex;
    flex-direction: row;
    font-size: 0.25rem;

    .ranking-left {
      flex: 1;
      text-align: center;
      transition: all 1s;
    }
    .ranking-right {
      flex: 3;
    }
    .ranking-out {
      border-radius: 0.15rem;
      height: 0.2rem;
      .ranking-inner {
        font-size: 0.18rem;
        height: 0.2rem;
        max-width: 100%;
        border-radius: 0.15rem;
        transition: all 1s;
        display: flex;
        align-items: center;
        justify-content: flex-end;
      }
    }
  }
}
</style>

