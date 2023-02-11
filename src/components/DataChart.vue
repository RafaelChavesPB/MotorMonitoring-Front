<template>
  <div>
    <Bar id="my-chart-id" :options="chartOptions" :data="mydata" />
  </div>
</template>

<script>
import io from "socket.io-client";
import { Bar } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
);

export default {
  name: "DataChart",
  components: { Bar },
  data() {
    return {
      mydata: {
        datasets: [{ data: [1, 2, 3, 4, 5, 6] }],
        label: ["a", "b", "c", "d", "e", "f"],
      },
      socket: {},
      chartOptions: {
        responsive: true,
      },
    };
  },
  created() {
    this.socket = io("http://localhost:3000");
  },
  mounted() {
    this.socket.on("new data", (params) => {
      // this.update(params);
    });
  },
  // computed:{
  //   chartData(){
  //     console.log(this.mydata.datasets[0].data)
  //     return this.mydata
  //   }
  // },
  methods: {
    update(params) {
      this.mydata.datasets[0].data.push(params.number);
      this.mydata.label.push(params.time);
      if (this.mydata.datasets[0].data.length > 40) {
        this.mydata.datasets[0].data.splice(0, 1);
        this.mydata.label.splice(0, 1);
      }
    },
  },
};
</script>