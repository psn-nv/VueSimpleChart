<template>
  <div>
    <span>{{data_array.title}}</span>
    <div>
      <svg id="piechart" :width="data_array.chartSize" :height="data_array.chartSize">
        <circle
          r="25%" cx="50%" cy="50%"
          v-for="(item,index) in dataArray" v-bind:key="index"
          v-bind:style="{strokeDasharray:`${item.len} ${item.empty}`, strokeDashoffset: item.offset, stroke: item.color, strokeWidth: item.pieSize}"
          :tt="item.empty"
        />
      </svg>
    </div>
  </div>
</template>

<script>
  export default {
    props:['data_array'],
    name: 'SimpleChart',
    data() { return { } },
    methods: { },
    computed: {
        circleLength(){
          return Math.PI * parseInt(this.data_array.chartSize) / 2;
        },
        dataArray(){
          let summed = 100 / this.data_array.data.reduce((pv,cv)=> pv += cv.value, 0);
          let startAt = 0;
          return this.data_array.data
            .sort((a,b)=> (this.data_array.isSortingByValue) ? a.value - b.value : 0)
            .map(itm =>{
              let tmp = { len : this.circleLength * itm.value * summed / 100,
                          percentage : itm.value * summed,
                          offset : -startAt,
                          color : itm.color,
                          name : itm.name,
                          pieSize : parseInt(this.data_array.chartSize) / 2
                        };
              startAt += tmp.len;
              tmp.empty = this.circleLength - tmp.len;
              return tmp;
          });
        }
    }
  }
</script>

<style scoped>
div{
  text-align: center;
}
div>div{
  margin: 20px auto;
}
#piechart{
  transform: rotate(-90deg);
  border-radius: 50%;
}
#piechart circle {
  fill:none;
}

</style>