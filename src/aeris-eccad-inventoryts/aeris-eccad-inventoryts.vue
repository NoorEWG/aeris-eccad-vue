/*
 dependances: 
*/

<template>
  <div>
    <br />
    <div class="etFlex">
      <aeris-eccad-category :service="categoryService" its="true"></aeris-eccad-category>
      <aeris-eccad-inventory :service="datasetService"></aeris-eccad-inventory>
      <div>
        <input type="button" class="etButton" @click="showTimeSeries()" value="Show time series"></input>
      </div>
    </div>
    <br />
    
    <div class="etExample" v-show="!showGraph">
        <div>
            <i class="fa fa-info-circle" style="height: 20px;"></i>
            <span>Please choose a datatype and inventory and click the button<br>Example:</span>
        </div>
        <img src="images/inventoryTimeseries.png">
    </div>

    <div class="etChart" v-show="showGraph">
      <aeris-eccad-inventorytschart identifier="itTotals" minmaxtotal="3"></aeris-eccad-inventorytschart>
      <aeris-eccad-inventorytschart identifier="itMax" minmaxtotal="2"></aeris-eccad-inventorytschart>
      <aeris-eccad-inventorytschart identifier="itMin" minmaxtotal="1"></aeris-eccad-inventorytschart>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    service: {
      type: String,
      default: ''
    },
  },
  
  data () {
    return {
      categoryService: 'http://eccad.aeris-data.fr/eccad2web/rest/data/categories',
      datasetService: 'http://eccad.aeris-data.fr/eccad2web/rest/data/parameters',
    	colors: {type: Array},
    	selectedColor: {type: Object},
      showGraph: false
    }
  },
  
  watch: {
  },
  
  mounted: function () {
  },
  
  updated: function() {
  },
  
  destroyed: function() { 
    document.removeEventListener('showITSGraph', this.setShowGraph);
  },
  
  created: function () {
    console.log("Aeris Eccad Emission Time Series - Creating");
    document.addEventListener('showITSGraph', this.setShowGraph);
  },
  
  computed: {
  },
  
  methods: {

    setShowGraph: function(evt) {
      this.showGraph = evt.detail;
    },
    
    showTimeSeries: function() {
      var ev1 = new CustomEvent('showITS', { 'detail': true });
      document.dispatchEvent(ev1); 
    }
  }
}
</script>

<style>	
</style>