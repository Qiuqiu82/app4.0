<template>
    <div class="content">
        <h1 class="wrapper">碳际汇</h1>

        <el-card id="chart_one" style="width: 90%; margin: 40px auto 0; height: 500px; box-shadow: 0 0 2px 2px #ccc;">
            <div>
                <div id="clothingPieChart" style="width: 100%; height: 400px;"></div>
            </div>
        </el-card>
        <div class="title2">点击查看您的超额比(跳转)</div>
        <div class="title3">推荐减排品牌</div>
        <div>
            <ul>
                <li>
                    <span class="hex first"><span class="hexIn"></span></span>
                </li>
                <li>
                    <span class="hex two"><span class="hexIn"></span></span>
                </li>
                <li>
                    <span class="hex three"><span class="hexIn"></span></span>
                </li>
            </ul>
            <div class="bigcircle">
                <div class="smallcircle">
                    <span>推荐衣物</span>
                </div>
            </div>
        </div>
        <el-dialog v-model="dialogFormVisible" title="衣物数据" width="500" :show-close="false">
            <el-form :model="clothingData">
              <el-form-item label="T恤" label-width="140px">
                <el-input v-model="clothingData[0].value" autocomplete="off" />
              </el-form-item>
              <el-form-item label="裤子" label-width="140px">
                <el-input v-model="clothingData[1].value" autocomplete="off" />
              </el-form-item>
              <el-form-item label="外套" label-width="140px">
                <el-input v-model="clothingData[2].value" autocomplete="off" />
              </el-form-item>
            </el-form>
            <template #footer>
              <div class="dialog-footer">
                <el-button type="primary" @click="renderChart">
                  确认
                </el-button>
              </div>
            </template>
          </el-dialog>

    </div>
</template>
  
<script>
import * as echarts from 'echarts';
export default {
  data() {
    return {
      dialogFormVisible: true,
      clothingData: [
        { name: 'T恤', value: 0 },
        { name: '裤子', value: 0 },
        { name: '外套', value: 0 },
      ],
    };
  },
  mounted() {
    this.initClothingPieChart();
  },
  methods: {
    renderChart() {
      this.dialogFormVisible = false;
      this.initClothingPieChart();
    },
    initClothingPieChart() {
      uni.createSelectorQuery()
        .in(this)
        .select('#clothingPieChart')
        .node()
        .exec((res) => {
          const canvas = res[0].node;
          if (canvas) {
            const myChart = echarts.init(canvas);

            const option = {
              title: {
                text: '月购物衣服数',
                subtext: '衣服类别分布',
                x: 'center',
              },
              tooltip: {
                trigger: 'item',
                formatter: '{a} <br/>{b}: {c} ({d}%)',
              },
              legend: {
                orient: 'vertical',
                left: 10,
                data: this.clothingData.map((item) => item.name),
              },
              series: [
                {
                  name: '购物数量',
                  type: 'pie',
                  radius: '55%',
                  center: ['50%', '60%'],
                  data: this.clothingData,
                  emphasis: {
                    itemStyle: {
                      shadowBlur: 10,
                      shadowOffsetX: 0,
                      shadowColor: 'rgba(0, 0, 0, 0.5)',
                    },
                  },
                },
              ],
            };

            myChart.setOption(option);
          }
        });
    },
  },
};
</script>
  
<style lang="scss">
.content {
    position: relative;
    min-width: 500px;

    // background-color: pink;
    .wrapper {
        margin: 10px 0px 0px 60px;
        background-image: -webkit-linear-gradient(top, #7c7c7c, #576667, #aa9c98);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        letter-spacing: 2px;
        color: #a00000;
        text-align: left;
        /* 文字设为透明 */
    }

    .title {
        margin: 0;
        text-align: center;
        font-size: 48px;
        letter-spacing: 8px;
        font-weight: 400;
        color: #6c6c6c;
        font-family: "Arial", "Verdana", "Helvetica", sans-serif;
        display: flex;
        align-items: center;
        justify-content: center;

        image {
            width: 40px;
            height: 40px;
        }
    }

    #chart_one {
        width: 90%;
        margin: 40px auto 0;
        height: 500px;
        box-shadow: 0 0 2px 2px #ccc;
    }

    .title2 {
        margin-top: 30px;
        text-align: center;
        font-size: 28px;
        letter-spacing: 2px;
        font-weight: 700;
    }

    .title3 {
        margin-top: 40px;
        font-size: 32px;
        letter-spacing: 8px;
        font-weight: 700;
        color: royalblue;
    }

    ul {
        position: relative;
        width: 180px;
        display: flex;
        flex-wrap: wrap;
        top: 30px;
    }

    ul li {
        // float: left;
        border-radius: 1px;
    }

    .hex {
        overflow: hidden;
        display: block;
        width: 70px;
        height: 78px;
        transform: rotate(-60deg) skewY(30deg);
        border-radius: 1px;
    }

    .hexIn {
        background-color: #ccc;
        display: block;
        width: 70px;
        height: 78px;
        line-height: 78px;
        text-align: center;
        border-radius: 1px;
        transform: skewY(-30deg) rotate(60deg);
    }

    .first {
        span {
            background-color: #27da9d;
            filter: brightness (12)
        }
    }

    .two {
        span {
            background-color: #f6c428;
        }
    }

    .three {
        position: relative;
        top: -25%;
        left: 45%;

        span {
            background-color: #4b7cfa;
        }
    }

    .bigcircle {
        position: relative;
        top: -150px;
        left: 400px;
        width: 150px;
        height: 150px;
        border-radius: 50%;
        background-color: #b8d2f5;

        .smallcircle {
            position: relative;
            top: 10px;
            width: 120px;
            height: 120px;
            border-radius: 50%;
            background-color: #3b7deb;
            text-align: center;
            line-height: 120px;

            text {
                position: absolute;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                font-size: 14px;
                font-weight: 700;
            }
        }
    }

    // .qq {

    // }
}
</style>