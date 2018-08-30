<template>
  <SimpleChart :data_array="paramsForChart" />
</template>

<script>
import SimpleChart from './SimpleChart';
export default {
  components: { SimpleChart },
  name: 'app',
  data() {
    return {
      paramsForChart:{title:'Header of test chart',
                        chartSize:'400px',
                        seriesLegendPosition:'bottom',
                        isSortingByValue:false,                      
                        data:[{name:"Data 1",value:111,color:"red"},
                              {name:"Data 2",value:143,color:"yellow"},
                              {name:"Data 3",value:90,color:"green"},
                              {name:"Data 4",value:10,color:"blue"},
                              {name:"Data 5",value:98,color:"teal"},
                              {name:"Data 6",value:50,color:"purple"},
                              {name:"Data 7",value:88,color:"#f9f"}
                              ]
                      }
    }
  }
}
</script>