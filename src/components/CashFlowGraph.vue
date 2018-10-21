<script>
import VueChart from 'vue-chartjs'
import moment from 'moment'
import axios from 'axios'

export default {
  extends: VueChart.Line,
  mixins: [VueChart.mixins.reactiveData],
  data () {
    return {
      chartData: {
        labels: [],
        datasets: [
          {
            label: 'Some Data!',
            backgroundColor: '#7af49b',
            data: []
          }
        ]
      }
    }
  },
  mounted () {
    // window.Chart.scaleService.updateScaleDefaults('linear', { ticks: { min: -100 }})
    window.Chart.defaults.global.defaultFontColor = 'rgba(210, 210, 210, 0.9)'
    window.Chart.defaults.global.defaultColor = 'rgba(210, 210, 210, 0.9)'

    axios.get('https://weekly-green.herokuapp.com/yodlee_mock.json').then(({ data }) => {
      let day = -1;
      let bals = [];
      let days = [];
      data.transactions.forEach((transaction) => {
        const { bal, date } = transaction;
        let newDay = moment(date).day();
        if (newDay !== day) {
          day = newDay;
          days.push(moment(transaction.date).toDate())
          bals.push(transaction.bal);
        }
      });

      this.chartData = {
        labels: days,
        datasets: [
          {
            label: 'Some Data!',
            backgroundColor: '#7af49b',
            data: bals
          }
        ]
      };
    });

    let nextTwoWeeksOfDates = [...Array(14)].map((_, i) => {
      return moment().add(i, 'days').format("dddd")
    })

    this.renderChart(this.chartData, {
			title: {
				display: true,
				text: 'Chart.js Time Point Data'
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
    })
  }
}
</script>

<style>
</style>
