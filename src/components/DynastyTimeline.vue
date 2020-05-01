<template>
  <div class="dynasty-timeline">
    <div v-html="dataHtml"></div>
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
    this.dataHtml = this.renderHtml();
  },
  methods: {
    renderHtml() {
      let timeline = this.timeline;
      let html = "";

      for (let i = 0; i < timeline.length; i++) {
        let yearData = timeline[i];

        if (typeof yearData == "undefined") {
          html +=
            '<div class="year-line"><div class="dynasty-line"></div></div>';
          continue;
        }

        html += '<div class="year-line">';
        for (let j = 0; j < yearData.length; j++) {
          let dynasty = yearData[j];
          html +=
            '<div class="dynasty-line bk' +
            this.getBackgroundIndex(i, dynasty.name) +
            '">';
          if (this.haveShow(i, dynasty.name)) {
            html += '<div class="dynasty-name">' + dynasty.name + "</div>";
          }
          html += "</div>";
        }
        html += "</div>";
      }
      return html;
    },
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
      dataHtml: "",
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
<style lang="scss">
.dynasty-timeline {
  margin-right: 20px;
  width: 120px;
  height: 100%;
}
.year-line {
  position: relative;
  display: flex;
  .dynasty-line {
    position: relative;
    width: 100%;
    height: 2px;
    background: #eee;
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
