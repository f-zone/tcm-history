<template>
  <div class="dynasty-timeline">
    <div v-for="(item, yearIdx) in timeline" :key="yearIdx" class="year-line">
      <div
        v-for="(dynasty, cdx) in item"
        :key="cdx"
        class="dynasty-line"
        :class="'bk' + getBackgroundIndex(yearIdx, dynasty.name)"
      >
        <div v-if="haveShow(yearIdx, dynasty.name)" class="dynasty-name">
          {{ dynasty.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DynastyTimeline",
  props: {
    dynastyData: Object
  },
  created() {
    this.timeline = this.dynastyData.timeline;
    console.info(777, this.timeline);
  },
  methods: {
    haveShow(yearIdx, name) {
      let ret = false;
      if (typeof this.nameShow[yearIdx - 1 + "_" + name] === "undefined") {
        ret = true;
      }
      this.nameShow[yearIdx + "_" + name] = true;
      return ret;
    },
    getBackgroundIndex(yearIdx, name) {
      // console.info(555, yearIdx, name);
      let ret = 0;
      if (typeof this.dynastyColor[yearIdx - 1 + "_" + name] !== "undefined") {
        ret = this.dynastyColor[yearIdx - 1 + "_" + name];
      } else {
        this.dynastyIndex++;
        ret = this.dynastyIndex % 5;
      }

      this.dynastyColor[yearIdx + "_" + name] = ret;
      return ret;
    }
  },
  data() {
    return {
      preYear: 0,
      dynastyColor: {},
      dynastyIndex: 0,
      nameShow: {},
      timeline: []
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.dynasty-timeline {
  width: 120px;
  height: 5000px;
}
.year-line {
  position: relative;
  display: flex;
  .dynasty-line {
    position: relative;
    width: 100%;
    height: 1px;
  }
  .dynasty-name {
    position: absolute;
    top: 0;
    left: 0;
    white-space: nowrap;
    font-size: 12px;
    color: #0645ad;
    z-index: 1;
  }
  .bk0 {
    background: rgb(255, 225, 255);
  }
  .bk1 {
    background: rgb(255, 236, 225);
  }
  .bk2 {
    background: rgb(255, 255, 225);
  }
  .bk3 {
    background: rgb(225, 255, 225);
  }
  .bk4 {
    background: rgb(193, 248, 247);
  }
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
