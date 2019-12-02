<template>
  <div>
    <div id="graph" style="width:100%;height:500px"></div>
  </div>
</template>
<script>
import echarts from "echarts/lib/echarts";
import "echarts/lib/chart/graph";

export default {
  data() {
    return {
      graph: "",
      pointData: [],
      linkData: [],
      categoryData: [],
      options: {
        title: {
          text: "知识图谱示例"
        },
        series: [
          {
            name: "知识图谱",
            type: "graph",
            layout: "force",
            force: {
              repulsion: 60,
              gravity: 0.1,
              edgeLength: 15,
              layoutAnimation: true
            },
            data: [],
            links: [],
            categories: [],
            roam: false,
            symbol: 'circle',
            symbolSize: 40,
            cursor: 'pointer',
            label: {
              normal: {
                show: true,
                position: "inside",
                formatter: "{b}",
                fontSize: 16,
                fontStyle: "600"
              }
            },
            lineStyle: {
              normal: {
                opacity: 0.9,
                width: 1.5,
                curveness: 0
              }
            }
          }
        ]
      }
    };
  },
  methods: {
    setPointData(list, category) {
      list.forEach((name, index) => {
        this.pointData.push({
          x: index * 50,
          y: 20 + index * 50,
          name,
          category,
          draggable: true
        });
      });
    },
    setLinkData(list, target) {
      list.forEach(source => {
        this.linkData.push({
          source,
          target,
          lineStyle: {
            normal: {
              color: "source"
            }
          }
        });
      });
    },
    setCategoryData(list) {
      list.forEach(name => {
        this.categoryData.push({ name });
      });
    }
  },
  created() {},
  mounted() {
    this.graph = echarts.init(document.getElementById("graph"));
    let pointList1 = ["红", "红1", "红2", "红3", "红4"];
    let pointList2 = ["蓝", "蓝1", "蓝2", "蓝3", "蓝4"];
    let pointList3 = ["黄", "黄1", "黄2", "黄3", "黄4"];
    let pointList4 = ["颜色"];
    this.setPointData(pointList1, "红");
    this.setPointData(pointList2, "蓝");
    this.setPointData(pointList3, "黄");
    this.setPointData(pointList4, "颜色");
    this.setLinkData(pointList1, "红");
    this.setLinkData(pointList2, "蓝");
    this.setLinkData(pointList3, "黄");
    this.setLinkData(["红", "蓝", "黄"], "颜色");
    this.setCategoryData(["红", "蓝", "黄", "颜色"]);
    this.options.series[0].data = this.pointData;
    this.options.series[0].links = this.linkData;
    this.options.series[0].categories = this.categoryData;
    // this.options.legend.data = this.categoryData;
    this.$nextTick(() => {
      window.console.log(this.options);
      this.graph.setOption(this.options);
    });
  }
};
</script>
<style scoped>
#graph {
}
</style>