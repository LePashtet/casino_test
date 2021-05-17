<template>
  <div class="rulet-wrp">
    <div class="rulet_view">
      <div class="rulet_view_result">{{ result }}</div>
      <img src="@/assets/arow.svg" alt="arrow" class="rulet_view_arrow" />
      <img src="@/assets/table.svg" alt="Table" class="rulet_view_table" />
      <img
        ref="rulet"
        src="@/assets/rulet.svg"
        alt="rulet"
        class="rulet_view_nums"
      />
    </div>
    <input
      type="button"
      :disabled="disable"
      id="btn"
      @click="run()"
      placeholder="Run"
      value="Run"
    />
  </div>
</template>

<script>
import anime from "animejs";

export default {
  name: "rulet",
  data: () => {
    return {
      result: null,
      ruletNumbers: [
        36, 13, 27, 6, 34, 17, 25, 2, 21, 4, 19, 15, 32, 0, 26, 3, 35, 12, 28,
        7, 29, 18, 22, 9, 31, 14, 20, 1, 33, 16, 24, 5, 10, 23, 8, 30, 11,
      ],
      disable: false,
      anim: null,
    };
  },
  methods: {
    run() {
      this.disable = true;
      this.result = Math.floor(Math.random() * 37);
      let rotate = (360 / 37) * this.ruletNumbers.indexOf(this.result) + 720;
      const targets = this.$refs.rulet;

      anime({
        targets,
        rotate: 0,
        easing: "easeOutExpo",
        duration: 0,
      });

      anime({
        targets,
        rotate,
        easing: "easeOutExpo",
        duration: 8000,
        complete: () => {
          this.disable = false;
        },
      });
    },
  },
  mounted() {
    this.run();
  },
};
</script>

<style scoped lang="scss">
.rulet-wrp {
  .rulet {
    &_view {
      position: relative;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      &_result {
        width: 60%;
        height: 60%;
        border-radius: 50%;
        background-color: gray;
        color: white;
        font-weight: 600;
        font-size: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
      }
      &_arrow {
        position: absolute;
        width: 15%;
        left: 43%;
        top: 18%;
      }
      &_nums {
        position: absolute;
        width: 80%;
        height: 80%;
      }
      &_table {
        position: absolute;
        width: 100%;
        height: 100%;
      }
    }
  }
}
</style>
