<template>
  <div class="header">
    <div v-html="dollarIcon"></div>
    <h1>Conversor de moeda</h1>
    <div v-html="dollarIcon"></div>
  </div>
</template>

<script>
import feather from "feather-icons";

export default {
  name: "Header",
  computed: {
    dollarIcon() {
      return feather.icons["dollar-sign"].toSvg();
    },
  },
};
</script>

<style scoped lang="less">
.header {
  height: 80px;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  background: @light-pink;

  h1 {
    margin: 0;
    font-weight: 400;
  }

  @media @smartphones {
    h1 {
      font-size: 1.5rem;
    }
  }
}
</style>
