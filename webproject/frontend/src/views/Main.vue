<template>
  <div>
      <Form></Form>
      <bar-chart style="width:30vw;" v-if="chartData" :chart-data="chartData"></bar-chart>
  </div>
</template>

<script>
// Main.vue
// mapActions 가져오기
import {mapState, mapActions } from "vuex"
import BarChart from "../components/ReactiveBarChart";
import Form from '../components/Form';
export default {
    components:{
        BarChart,
        Form
    },
    data(){
        return {
            // data에있는 chartData 주석처리
            // chartData: null
        }
    },
    // mapState는 computed에서 가져온다
    computed:{
        ...mapState( [ 'chartData' ] )
    },
    methods:{
        // actions가 아닌 방식의 action 호출
        // this.$store.dispatch 로 호출
        // mapActions 넣기
        ...mapActions(["generateChartData"]),
        generateData(){
            let newArray = [];
            let newArray2 = [];
            
            for(let i =0; i< 10; i ++){
                let randomValue = Math.floor(Math.random() * 10);
                newArray.push(randomValue);
            }

            for(let i =0; i< 10; i ++){
                let randomValue = Math.floor(Math.random() * 10);
                // 1 -> 2
                newArray2.push(randomValue);
            }

            this.chartData = {
                labels: ["Red", "Blue", "Yello", "Green", "Purple", "Orange"],
                datasets: [
                    {
                        label: "Data One",
                        backgroundColor:"#f87979",
                        data: newArray,
                        fill: false
                    },
                                        {
                        label: "Data Two",
                        backgroundColor:"black",
                        // 1 -> 2
                        data: newArray2,
                        fill: false
                    }
                ]
            }
        }
    },

    async mounted() {
        // this.generateData();
        // setInterval(this.generateData, 2000);
        this.generateChartData();
    },

}
</script>

<style>

</style>