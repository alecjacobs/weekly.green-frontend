<template>
  <CashFlowGraph :height="150" :chartData="cashFlowHistory" :options="options" />
</template>

<script>
  import CashFlowGraph from '../components/CashFlowGraph'
  import moment from 'moment'
  import axios from 'axios'

  export default {
    components: {
      CashFlowGraph
    },
    data () {
      return {
        cashFlowHistory: {},
        options: {}
      }
    },
    mounted () {
      axios.get('https://weekly-green.herokuapp.com/yodlee_mock.json').then(({ data }) => {
        let day = -1;
        let bals = [];
        data.transactions.forEach((transaction) => {
          const { bal, date } = transaction;
          let newDay = moment(date).day();
          if (newDay !== day) {
            day = newDay;
            bals.push({ y: bal + 1000.0, t: date });
          }
        });

        this.cashFlowHistory = {
          datasets: [
            {
              label: 'Transaction History',
              backgroundColor: '#7af49b',
              data: bals
            }
          ]
        };

        this.options = {
          legend: {
            display: false
          },
          scales: {
            xAxes: [{
              type: 'time',
              display: true,
              scaleLabel: {
                display: false
              },
              ticks: {
                major: {
                  fontStyle: 'bold',
                  fontColor: '#FF0000'
                }
              }
            }],
            yAxes: [{
              display: true,
              scaleLabel: {
                display: true,
                labelString: 'Your Balance'
              }
            }]
          }
        };
      });
    }
  }
</script>
