/*
 dependances: 
*/

<template>
  <div class="selectionFlex" v-show="!hideSelectionBar">
      <div class="selectionColumn">
        <div class="selectionRow"> 
          <div class="selectItem">
            <aeris-eccad-category :service="categoryService" first="true"></aeris-eccad-category>
          </div>
          <div class="selectItem">
            <aeris-eccad-scenario :service="scenarioService" first="true"></aeris-eccad-scenario>
          </div>
        </div>   
        <div class="selectionRow">   
          <div class="selectItem">
            <aeris-eccad-parameter :service="parameterService" first="true"></aeris-eccad-parameter>
          </div>
          <div class="selectItem">
            <aeris-eccad-sector :service="sectorService" first="true"></aeris-eccad-sector>   
          </div> 
        </div>
        <div class="selectionRow"> 
          <div class="selectItem">
            <aeris-eccad-dataset :service="datasetService" first="true"></aeris-eccad-dataset>
          </div>
          <div class="selectItem">
            <aeris-eccad-date first="true"></aeris-eccad-date>
          </div>
        </div>
        <div class="selectionRow"> 
          <div class="selectItem">
            <aeris-eccad-resolution :service="resolutionService" first="true"></aeris-eccad-resolution>
          </div>
        </div>
  
        <aeris-eccad-reset-compare></aeris-eccad-reset-compare> 
         
        <div class="selectionRow"> 
          <div class="selectItem">
            <aeris-eccad-category :service="categoryService" first="false"></aeris-eccad-category>
          </div>
          <div class="selectItem">
            <aeris-eccad-scenario :service="scenarioService" first="false"></aeris-eccad-scenario>
          </div>
        </div>   
        <div class="selectionRow">   
          <div class="selectItem">
            <aeris-eccad-parameter :service="parameterService" first="false"></aeris-eccad-parameter>
          </div>
          <div class="selectItem">
            <aeris-eccad-sector :service="sectorService" first="false"></aeris-eccad-sector>   
          </div> 
        </div>
        <div class="selectionRow"> 
          <div class="selectItem">
            <aeris-eccad-dataset :service="datasetService" first="false"></aeris-eccad-dataset>
          </div>
          <div class="selectItem">
            <aeris-eccad-date first="false"></aeris-eccad-date>
          </div>
        </div>
        <div class="selectionRow"> 
          <div class="selectItem">
            <aeris-eccad-resolution :service="resolutionService" first="false"></aeris-eccad-resolution>
          </div>
        </div>
      </div>

      <div class="selectionDrawColumn">
        <div class="selectionDrawRow">
          <div class="selectItemH">
            <aeris-eccad-rb-unit :service="unitService"></aeris-eccad-rb-unit> 
          </div>
          <div class="selectItemH">  
            <aeris-eccad-mask :service="maskService"></aeris-eccad-mask>
            <aeris-eccad-geospatial :service="geospatialService"></aeris-eccad-geospatial>
          </div>
        </div>
        <div class="selectionDrawRow">
            <aeris-eccad-drawbuttons></aeris-eccad-drawbuttons> 
            <aeris-eccad-bbox></aeris-eccad-bbox>
        </div>
        <div class="selectionDrawRow">
          <div class="selectItem">
            <aeris-eccad-rb-unit :service="unitService" first="false" group="ft2"></aeris-eccad-rb-unit> 	
          </div>
        </div>
      </div>
 
      <div class="selectionColumn">
        <div class="selectionRow">
          <div class="selectItem">
            <aeris-eccad-color :service="colorService"></aeris-eccad-color>
          </div>
          <div class="selectItem">
            <aeris-eccad-numcolors></aeris-eccad-numcolors>
          </div>
        </div>
        <div class="selectionRow">  
          <div class="selectItem">
            <aeris-eccad-range></aeris-eccad-range>
          </div>
          <div class="selectItem">  
            <aeris-eccad-scale></aeris-eccad-scale>
          </div>
        </div>  
        <div class="selectionRow">  
          <div class="selectItem">
            <aeris-eccad-min></aeris-eccad-min>
          </div>
          <div class="selectItem">  
            <aeris-eccad-max></aeris-eccad-max>
          </div>
        </div>

        <aeris-eccad-comparebox></aeris-eccad-comparebox>
        
        <div class="selectionRow">    
          <div class="selectItem">
            <aeris-eccad-min first="false"></aeris-eccad-min>
          </div>
          <div class="selectItem">  
            <aeris-eccad-max first="false"></aeris-eccad-max>
          </div>
        </div>
      </div>
  </div>     
</template>
  
<script>
import { EventBus } from '../aeris-event-bus/aeris-event-bus.js';
export default {
  props: {
    first: {
      type: Boolean,
      default: true
    },
    service: {
      type: String    
    }
  },
  
  data () {
    return {
      hideSelectionBar : false,
      categoryService: this.service + 'data/categories',
      parameterService: this.service + 'data/parameters',
      scenarioService: this.service + 'data/scenarios',
      datasetService: this.service + 'data/inventories',
      sectorService: this.service + 'data',
      unitService: this.service + 'data/totalunit',
      maskService: this.service + 'dataanalysis/masks',
      colorService: this.service + 'data/colors',
      geospatialService: this.service + 'data/geospatial',
      resolutionService: this.service + 'dataanalysis/resolutions'
    }
  },
  
  watch: {
  },
  
  mounted: function () {
  },
  
  updated: function() {
  },
  
  destroyed: function() {
     document.removeEventListener('hideSelectionBar', this.setHideSelectionBar);
  },
  
  created: function () {
    console.log("Aeris Eccad Selection Bar - Creating");
    document.addEventListener('hideSelectionBar', this.setHideSelectionBar);
  },
  
  computed: {
  },
  
  methods: {
    setHideSelectionBar: function(evt) {
       this.hideSelectionBar = evt.detail; 
    }
  }
}
</script>

<style>

	
</style>
