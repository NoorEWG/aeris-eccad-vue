/*
 dependances: 
*/

<template>
  <nav class="navbarEccad" data-ng-controller="menuCtrl">
        <div class="menuEccad">
            <div>
                <ul class="menuEccadUl">
                    <li class="menuItemEccad" v-bind:key="link.menu" v-for="link in links">
                         <div class="menu" @click="change(link.menu)">{{ link.text }}</div>
                    </li>
                </ul>           
            </div>
             
            <div v-if="showCategories">
                <span v-bind:key="catgroup.id" v-for="catgroup in categoryGroups">
                    <label class="spacedradiobutton categoryGroupButtons" :class="{color: catgroup.color}">
                        <input type="radio" name="categoryGroup" :value="catgroup.id" v-model="categoryGroupId" @click="changeCategoryGroup()" />{{catgroup.name}}
                    </label>
                </span>
            </div>
            <div class="hideShow">
                <a v-if="!hideheader"><img src="images/hide.png" alt="hide" @click="hideHeader(true)" /></a>
                <a v-if="hideheader"><img src="images/show.png" alt="show" @click="hideHeader(false)" /></a>
            </div>
        </div>
    </div>    
  </nav>
</template>

<script>
export default {
  props: {
  },
  
  data () {
    return {
      links: [],
      categoryGroups: [],  
      categoryGroupId: 1,
      categoryGroup: {},
      showCategories : false,
      selectedLink: {},
      hideheader: false    
    }
  },
  
  watch: {
    selectedLink (value) {
        if(value.menu === 'catalog') {
            this.showCategories = true;
        }
        else {
            this.showCategories = false;
        }
    }, 
  },
  
  mounted: function () {
  },
  
  updated: function() {
  },
  
  destroyed: function() {
    document.removeEventListener('catalogmenu', this.setLinkCatalogMenu);
    document.removeEventListener('toolsmenu', this.setLinkToolsMenu);
    document.removeEventListener('catGroups', this.setCategoryGroups);
  },
  
  created: function () {
    console.log("Aeris Eccad Main Menu - Creating");
    this.links = [
      {url: '', text: 'Home', menu: 'home', restricted: false},
      {url: '', text: 'Catalogue', menu: 'catalog', restricted: false},
      {url: '', text: 'Online-Tools', menu: 'tools', restricted: false},
      {url: '', text: 'Admin', menu: 'admin', restricted: true},
      {url: '', text: 'Help', menu: 'help', restricted: false},
    ];
    this.selectedLink = this.links[0];
    //EventBus.$on('mainmenu', data => {
    //    this.selectedLink = JSON.parse(data)
	//});
    document.addEventListener('catalogmenu', this.setLinkCatalogMenu);
    document.addEventListener('toolsmenu', this.setLinkToolsMenu);
    document.addEventListener('catGroups', this.setCategoryGroups);

  },
  
  computed: {
  },
  
  methods: {
    
    setLinkCatalogMenu: function(evt) {
        this.selectedLink = evt.detail;
    },
    
    setLinkToolsMenu: function(evt) {
        this.selectedLink = evt.detail;
    },
    
    setCategoryGroups: function(evt) {
        this.categoryGroups = evt.detail;
    },
    
    change: function(menu) {
        
        var ev1 = new CustomEvent('mainmenu', { 'detail': menu});
        document.dispatchEvent(ev1); 
        if(menu === 'catalog') {
           this.showCategories = true;
        }
        else {
            this.showCategories = false;
        }

    },

    changeCategoryGroup: function() {
        var ev2 = new CustomEvent('categoryGroup', { 'detail': this.categoryGroup });
        document.dispatchEvent(ev2);   
    },

    hideHeader: function(bool) {
        this.hideheader = bool;
        var ev3 = new CustomEvent('hideMainHeader', { 'detail': bool });
        document.dispatchEvent(ev3); 
    }  
  }
}
</script>

<style>
</style>