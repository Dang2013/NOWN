<template>
  <div>
    <div style="display: flex; justify-content:center; ">
      <button style="margin-right:30px;" @click="ClickBtn(1)">알별</button>
      <button style="margin-right:30px;" @click="ClickBtn(2)">주별</button>
      <button style="margin-right:30px;" @click="ClickBtn(3)">월별</button>
    </div>
    <Line
      :chart-options="chartOptions"
      :chart-data="SevenData.chartData"
      :chart-id="chartId"
      :plugins="plugins"
      :css-classes="cssClasses"
      :styles="styles"
      :width="width"
      :height="height"
    />
</div>
</template>

<script>
// http://127.0.0.1:8000/PX/weightgraph/day
import { Line } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  PointElement,
  CategoryScale
} from 'chart.js'
import { onMounted, onUpdated, reactive } from '@vue/runtime-core'
import { useStore } from 'vuex'

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  PointElement,
  CategoryScale
)

export default {
  name: 'LineChart',
  components: {
    Line
  },
  props: {
    chartId: {
      type: String,
      default: 'line-chart'
    },
    width: {
      type: Number,
      default: 900
    },
    height: {
      type: Number,
      default: 600
    },
    cssClasses: {
      default: '',
      type: String
    },
    styles: {
      type: Object,
      default: () => {}
    },
    plugins: {
      type: Array,
      default: () => []
    }
  },

  setup (props) {
    const store = useStore()
    store.dispatch('getWeightDay', localStorage.getItem('userPk'))
    const aa = store.state.diet
    const SevenData = reactive({
      chartData: {
        labels: ['8월 11일', '8월 12일', '8월 13일', '8월 14일', '8월 15일', '8월 16일', '8월 17일'],
        datasets: [
          {
            label: '체중',
            backgroundColor: 'blue',
            data: [65, 62, 59, 58, 65, 64, 61]
          },
          {
            label: '목표체중',
            backgroundColor: 'red',
            data: [55, 52, 51, 53, 55, 54, 53]
          }
        ]
      }
    })
    function ClickBtn (a) {
      if (a === 1) {
        store.dispatch('getWeightDay', localStorage.getItem('userPk'))
      } else if (a === 2) {
        store.dispatch('getWeightWeek', localStorage.getItem('userPk'))
      } else {
        store.dispatch('getWeightMonth', localStorage.getItem('userPk'))
      }
      for (let index = 0; index < store.state.diet.weightSeven.length; index++) {
        SevenData.chartData.labels[index] = store.state.diet.weightSeven[index].date
        SevenData.chartData.datasets[0].data[index] = store.state.diet.weightSeven[index].weight
        SevenData.chartData.datasets[1].data[index] = store.state.diet.weightSeven[index].object_weight
      }
    }
    for (let index = 0; index < store.state.diet.weightSeven.length; index++) {
      SevenData.chartData.datasets[0].data[index] = store.state.diet.weightSeven[index].weight
      SevenData.chartData.datasets[1].data[index] = store.state.diet.weightSeven[index].object_weight
    }
    onMounted(() => {
      store.dispatch('getWeightDay', localStorage.getItem('userPk'))
      for (let index = 0; index < store.state.diet.weightSeven.length; index++) {
        SevenData.chartData.datasets[0].data[index] = store.state.diet.weightSeven[index].weight
        SevenData.chartData.datasets[1].data[index] = store.state.diet.weightSeven[index].object_weight
      }
    })
    onUpdated(() => {
      store.dispatch('getWeightDay', localStorage.getItem('userPk'))
      for (let index = 0; index < store.state.diet.weightSeven.length; index++) {
        SevenData.chartData.datasets[0].data[index] = store.state.diet.weightSeven[index].weight
        SevenData.chartData.datasets[1].data[index] = store.state.diet.weightSeven[index].object_weight
      }
    })
    const chartOptions = {
      responsive: true,
      maintainAspectRatio: false
    }

    return { chartOptions, SevenData, aa, ClickBtn }
  }
}
</script>

<style scope>
.button-container{
  display:block;
  margin:auto;
  /* display:inline-block; */
}
button{
  /* background-color: var(--color-grey-900); */
  color: #6dcef5;

  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  font-family: 'MaruBuriOTF';
  font-style: normal;
  border-width: 0;
  width: 70px;
  height: 30px;
  font-size: 20px;
  text-align: center;
  font-weight: bold;
}

button:hover {
  background-color: #6dcef5;
  color: white;
  font-weight: bold;
}

button.disabled{
  cursor: default;
  background-color: var(--color-grey-100);
  border: 2px solid var(--color-grey-500);
  color: var(--color-grey-500);
}
</style>
