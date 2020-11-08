<template lang="html">
  <v-container>
    <h1>Neil's app</h1>
    <v-row>
      <v-col>
        <v-card>
          <v-card-title>Pearson regression calculator</v-card-title>
          <v-text-field  class='mx-12' placeholder='enter data set 1' v-model='inputOne'></v-text-field>
          <v-btn class='mx-12' @click='pushToArrayOne'>Add data</v-btn>
          <v-text-field  class='mx-12'placeholder='enter data set 2' v-model='inputTwo'></v-text-field>
          <v-btn class='mx-12 mb-12' @click='pushToArrayTwo'>Add data</v-btn>
          <v-divider></v-divider>
          <v-btn class='mx-12 my-12' @click='arithmeticMean'>Calculate Pearson Regression</v-btn>
          <v-btn class='mx-12 my-12' @click='getStandardDeviation(dataSetOne, meanOne)'>Stan Dev</v-btn>
          <v-btn class='mx-12 my-12' @click='getCoVariance(dataSetOne, dataSetTwo)'>Co Variance</v-btn>
        </v-card>
        <v-card class='mt-12'>
          <v-card-title >Results</v-card-title>
          <p>{{dataSetOne}}</p>
          <p>{{dataSetTwo}}</p>
          <p>Mean One: {{meanOne}}</p>
          <p>Mean Two: {{meanTwo}}</p>
          <p>Stan Dev: {{stanDev}}</p>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    inputOne: 30,
    inputTwo: 40,
    dataSetOne: [],
    dataSetTwo: [],
    meanOne: 0,
    meanTwo: 0,
    stanDev: 0,


  }),
  methods: {
    pushToArrayOne: function () {
      this.dataSetOne.push(parseInt(this.inputOne));
    },
    pushToArrayTwo: function () {
      this.dataSetTwo.push(parseInt(this.inputTwo));
    },
    arithmeticMean: function () {
      this.meanOne = this.getMean(this.dataSetOne);
      this.meanTwo = this.getMean(this.dataSetTwo);
    },
    getMean: function (array) {
      var set = array;
      var sum = set.reduce(function(a,b){
        return a+b;
      },0)
      return sum/set.length;;
    },
    getStandardDeviation: function (array, mean) {
      var set = array;
      var m = mean;
      var sumDeviations = 0;
      for(var i in set){
        sumDeviations += Math.pow((set[i]-m),2);
      }
      this.stanDev = Math.sqrt(sumDeviations/set.length);
    },
    getCoVariance: function (array1 ,array2){
      var set = array1;
      var m1 = this.getMean(array1);
      var m2 = this.getMean(array2);
      var sums = 0;
      for(var i in array1){
        sums += ((array1[i]-m1)*(array2[i]-m2));
      }
      console.log(sums);
      var cV = sums/array1.length;

    }


  }
}
</script>

<style lang="css" scoped>
</style>
