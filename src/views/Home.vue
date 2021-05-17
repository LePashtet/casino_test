<template>
  <div class="home">
    <rulet class="rulet" />
    <bidBoard class="bidBoard" />
  </div>
</template>

<script>
// @ is an alias to /src
import bidBoard from "@/components/bidBoard";
import rulet from "@/components/rulet";

export default {
  name: "Home",
  components: {
    bidBoard,
    rulet,
  },
};
</script>
<style lang="scss">
.home {
  .bidBoard {
    width: 600px;
    margin: 0 auto;
  }
  .rulet {
    width: 320px;
    height: 320px;
    margin: 0 auto;
  }
}
</style>
