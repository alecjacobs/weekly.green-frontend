<template>
  <CashFlowGraph :height="150" :chartData="cashFlowHistory" />
</template>

<script>
  import axios from 'axios'
  import moment from 'moment'
  import CashFlowGraph from '../components/CashFlowGraph'

  export default {
    components: {
      CashFlowGraph
    },
    data () {
      return {
        cashFlowHistory: {}
      }
    },
    mounted () {
      axios.get('https://weekly-green.herokuapp.com/yodlee_mock.json').then(({ data }) => {
        let day = -1;
        let bals = [];
        let days = [];
        data.transactions.forEach((transaction) => {
          const { bal, date } = transaction;
          let newDay = moment(date).day();
          if (newDay !== day) {
            day = newDay;
            days.push(moment(transaction.date).toDate());
            bals.push({ y: transaction.bal + 1000.0, t: date });
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
      });
    }
  }
</script>
