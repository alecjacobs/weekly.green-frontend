<template>
  <v-container flex><v-layout>
    <v-flex xs6>
      <CashFlowGraph :height="150" :chartData="cashFlowHistory" :options="options" />
    </v-flex>
    <v-flex xs6>
      <CashFlowGraph :height="150" :chartData="future" :options="options" />
    </v-flex>
  </v-layout></v-container>
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
        future: {},
        options: {}
      }
    },
    mounted () {
      axios.get('https://weekly-green.herokuapp.com/yodlee_mock.json').then(({ data }) => {
        let day = -1;
        let bals = [];
        let future = [];
        data.transactions.forEach((transaction) => {
          const { bal, date } = transaction;
          let newDay = moment(date).day();
          if (newDay !== day) {
            day = newDay;
            bals.push({ y: bal + 1000.0, t: moment(date) });
            future.push({ y: bal + 1000.0, t: moment(date).add(90, 'days') });
          }
        });

        let i = 0;
        let b = bals[bals.length - 1].y;
        this.future = {
          datasets: [
            {
              label: 'Transaction History',
              backgroundColor: '#aaa',
              data: future.map(({ y, t }) => {
                i = i + 1;
                b = b + (Math.random() - 0.5) * 50.0;
                return { y: b, t: t.add(i, 'days') };
              })
            },
            {
              label: 'Transaction History',
              backgroundColor: '#bbb',
              data: future.map(({ y, t }) => {
                i = i + 1;
                b = b + (Math.random() - 0.5) * 40.0;
                return { y: b, t: t.add(i, 'days') };
              })
            },
            {
              label: 'Transaction History',
              backgroundColor: '#ccc',
              data: future.map(({ y, t }) => {
                i = i + 1;
                b = b + (Math.random() - 0.5) * 30.0;
                return { y: b, t: t.add(i, 'days') };
              })
            }
          ]
        };

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
                display: false,
                labelString: 'Your Balance'
              }
            }]
          }
        };
      });
    }
  }
</script>
