<template>
  <div class="bidBoard-wrp">
    <div class="bidBoard-item_select" v-if="selected.length">
      Selected {{ selected.toString() }}
      <span @click="clearSelected"
        >Restore? <img src="@/assets/refresh-line.svg" alt=""
      /></span>
    </div>
    <div
      class="bidBoard-item zero"
      :class="isActive(0)"
      @click="selectOne([0])"
    >
      0
    </div>
    <div
      class="bidBoard-item number"
      :key="item"
      v-for="item in 36"
      :style="{ gridArea: 'n' + item.toString(), background: setColor(item) }"
      :class="isActive(item)"
      @click="selectOne([item])"
    >
      {{ item }}
    </div>
    <div
      class="bidBoard-item filter"
      :key="item.text"
      v-for="(item, index) in filters"
      :class="item.class"
      :style="{ gridArea: 'f' + index.toString() }"
      @click="select(item.val)"
      @mouseenter="setActive(item.val)"
      @mouseleave="clearActive()"
    >
      {{ item.text }}
    </div>
  </div>
</template>

<script>
export default {
  name: "bidBoard",
  data: () => {
    return {
      filters: [
        {
          text: "1 to 12",
          val: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
          class: "x4",
        },
        {
          text: "13 to 24",
          val: [13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24],
          class: "x4",
        },
        {
          text: "25 to 36",
          val: [25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36],
          class: "x4",
        },
        {
          text: "1 to 18",
          val: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18],
          class: "x2",
        },
        {
          text: "Even",
          val: [
            2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36,
          ],
          class: "x2",
        },
        {
          text: "Red",
          val: [
            1, 3, 5, 7, 9, 12, 14, 16, 18, 19, 21, 23, 25, 27, 30, 32, 33, 34,
            36,
          ],
          class: "redBtn",
        },
        {
          text: "Black",
          val: [2, 4, 6, 8, 10, 11, 13, 15, 17, 20, 22, 24, 26, 28, 29, 31, 35],
          class: "blackBtn",
        },
        {
          text: "Odd",
          val: [1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 35],
          class: "x2",
        },
        {
          text: "19 to 36",
          val: [
            19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35,
            36,
          ],
          class: "x2",
        },
        {
          text: "1:1",
          val: [3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 33, 36],
          class: "x1",
        },
        {
          text: "2:1",
          val: [2, 5, 8, 11, 14, 17, 20, 23, 26, 29, 32, 35],
          class: "x1",
        },
        {
          text: "3:1",
          val: [1, 4, 7, 10, 13, 16, 19, 22, 25, 28, 31, 34],
          class: "x1",
        },
      ],
      red: [
        1, 3, 5, 7, 9, 12, 14, 16, 18, 19, 21, 23, 25, 27, 30, 32, 33, 34, 36,
      ],
      black: [2, 4, 6, 8, 10, 11, 13, 15, 17, 20, 22, 24, 26, 28, 29, 31, 35],
      active: [],
      selected: [],
    };
  },
  methods: {
    setColor(num) {
      return this.red.indexOf(num) !== -1 ? "#ac0303" : "#2c3e50";
    },
    isActive(num) {
      return this.active.indexOf(num) !== -1 ||
        this.selected.indexOf(num) !== -1
        ? "hover"
        : "";
    },
    selectOne(num) {
      num.forEach((i) => {
        let index = this.selected.indexOf(i);
        if (index !== -1) {
          this.selected.splice(index, 1);
        } else {
          this.selected.push(i);
        }
      });
    },
    select(num) {
      num.forEach((i) => {
        let index = this.selected.indexOf(i);
        if (index === -1) {
          this.selected.push(i);
        }
      });
    },
    clearSelected() {
      this.selected = [];
    },
    setActive(num) {
      this.active.push(...num);
    },
    clearActive() {
      this.active = [];
    },
  },
  computed: {},
};
</script>

<style scoped lang="scss">
.bidBoard-wrp {
  color: white;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 40px 40px 40px 40px 40px 40px;
  gap: 10px 5px;
  grid-template-areas:
    "selected selected selected selected selected selected selected selected selected selected selected selected selected selected"
    "zero n3 n6 n9 n12 n15 n18 n21 n24 n27 n30 n33 n36 f9"
    "zero n2 n5 n8 n11 n14 n17 n20 n23 n26 n29 n32 n35 f10"
    "zero n1 n4 n7 n10 n13 n16 n19 n22 n25 n28 n31 n34 f11"
    ". f0 f0 f0 f0 f1 f1 f1 f1 f2 f2 f2 f2 ."
    ". f3 f3 f4 f4 f5 f5 f6 f6 f7 f7 f8 f8 .";

  .bidBoard-item {
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 10px;
    cursor: pointer;
    filter: saturate(300%);

    &:hover,
    &.hover {
      filter: saturate(100%);
    }

    &.zero {
      grid-area: zero;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #1bb108;
    }

    &.filter {
      border: 1px solid #c6c6c6;

      &:hover {
        background-color: rgb(#fff, 0.5);
      }
      &.redBtn {
        background-color: #ac0303;
        border: none;

        &:hover {
          background-color: rgb(#ac0303, 0.5);
        }
      }

      &.blackBtn {
        background-color: #2c3e50;
        border: none;

        &:hover {
          background-color: rgb(#2c3e50, 0.5);
        }
      }
    }


    &_select {
      grid-area: selected;
      text-align: center;
    }
  }
}
</style>
