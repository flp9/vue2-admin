<template>
  <div class="hello">
    <!--    <cander-test></cander-test>-->
    <Calendar
      v-on:choseDay="clickDay"
      v-on:changeMonth="changeDate"
      v-on:isToday="clickToday"
      v-on:markDate=arr
      v-on:topText=topText
    ></Calendar>
    <!--    :markDate=arr // arr=['2018/4/1','2018/4/3'] 标记4月1日和4月3日 简单标记-->
    <!--    :markDateMore=arr // 多种不同的标记-->
    <!--&lt;!&ndash;    第一个标记和第二个标记不能同时使用&ndash;&gt;-->
    <!--     :agoDayHide='1514937600' //某个日期以前的不允许点击  时间戳10位-->
    <!--     :futureDayHide='1525104000' //某个日期以后的不允许点击  时间戳10位-->
    <!--     :sundayStart="true" //默认是周一开始 当是true的时候 是周日开始-->
  </div>
</template>

<script>
  import Calendar from '_vue-calendar-component@2.8.2@vue-calendar-component'
  export default {
    name: 'CalendarTest',
    components: {Calendar},
    data() {
      return {
        arr: [{date: '2019/6/19', className: 'mark1'}, {date: '2019/6/12', className: 'mark2'}],
        chooseDayArr: [],
        topText: ['星期1', '星期2', '星期3', '星期4', '星期5', '星期6', '星期7']
      }
    },
    methods: {
      clickDay(data) {
        const chooseDay = this.chooseDayArr;
        const chooseDayLen = chooseDay.length;
        // this.chooseDayArr.push(data)
        // 默认选中的日期不重复
        if (chooseDayLen > 0) {
          var flag = false;
          for (let t in chooseDay) {
            if (chooseDay[t] === data) {
              flag = true;
              return false;
            }
          }
          if (!flag) {
            this.chooseDayArr.push(data)
          }
        } else {
          this.chooseDayArr.push(data)
        }
        console.log('选中日期数组集合--clickDay', this.chooseDayArr)
      },
      changeDate(data) {
        // 左右点击切换月份
        console.log('左右点击切换月份--changeDate', data);
      },
      clickToday(data) {
        // 跳到了本月
        console.log('跳到了本月--clickToday', data);
      }

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .mark1{
    background-color: red;
  }
  .mark1{
    background-color: bisque;
  }
</style>
