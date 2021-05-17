<template>
  <div class="rulet-wrp">
    <div class="rulet_view">
      <div class="rulet_view_result">{{ result }}</div>
      <img src="@/assets/arow.svg" alt="arrow" class="rulet_view_arrow" />
      <img
        ref="rulet"
        src="@/assets/rulet.svg"
        alt="rulet"
        class="rulet_view_nums"
      />
    </div>
    <button :disabled="disable" id="btn" @click="run">Run</button>
  </div>
</template>

<script>
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
      anime: null,
    };
  },
  methods: {
    run() {
      this.disable = true;
      this.result = Math.floor(Math.random() * 37);
      // this.$anime();
    },
  },
  mounted() {
    const targets = this.$refs.rulet;

    const btn = document.getElementById("btn");
    btn.onclick = () => {
      this.$anime
        .timeline()
        .add({
          targets,
          rotate: 0,
          direction: "normal",
          easing: "easeOutExpo",
          duration: 0,
        })
        .add({
          targets,
          rotate: (360 / 37) * this.coef + 720,
          easing: "easeOutExpo",
          duration: 8000,
          complete: () => {
            this.disable = false;
          },
        });
    };
  },
  computed: {
    coef() {
      return this.ruletNumbers.indexOf(this.result);
    },
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
        width: 50%;
        height: 50%;
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
        top: 22%;
      }
      &_nums {
        position: absolute;
        width: 312px;
        height: 312px;
      }
    }
  }
}
</style>
