<template>
  <div class="container">
    <div class="timeline-box">
      <DynastyTimeline :dynastyData="dynastyData" />
    </div>
    <div class="events-box"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import historyData from "@/data/history";
import DynastyTimeline from "@/components/DynastyTimeline.vue";

export default {
  name: "Home",
  components: { DynastyTimeline },
  created() {
    console.info(111, historyData.historyCN);
  },
  data() {
    return {
      dynastyData: historyData.historyCN
    };
  }
};
</script>
<style lang="scss">
.container {
  width: 100%;
  display: flex;
  .timeline-box {
    flex-grow: 1;
    border-right: 1px solid #ccc;
  }
  .events-box {
    width: 61.8%;
  }
}
</style>
