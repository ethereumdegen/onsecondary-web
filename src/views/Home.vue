<template>

<div>

   <div class="section  bg-gray-200  border-b-4 border-black px-0 lg:px-1">

     <div class=" ">
        <Navbar 
        v-bind:web3Plug="web3Plug"
        
       />
     </div>


   </div>

  

   <div class="section  border-b-2 border-black" style="background:#eee;">
     <div class=" ">
       <div class=" ">

       </div>
       <div class="  flex lg:flex-row flex-col  ">
 
         <div class="    w-full mt-8 py-8  px-1  text-center">

            <div class="  text-gray-900 text-xl my-4 px-16"> OnSecondary is a premium NFT Marketplace with 1% fee and revenue sharing paid out to the Community.   </div> 
 
           

        <div class="margin:0 auto; " style="">

          <div class="inline-block">
           <div  class="border-8 border-black p-2 m-2 "  style=" max-width:600px">
              <a href="https://market.onsecondary.com" target='_blank'>
               <img :src="getImgUrl('OnSecondaryMarketPromo.png')" class="p-2" style="height:400px"/>
              </a>

             
          </div>
           <a href="https://market.onsecondary.com" target='_blank'>
                https://market.onsecondary.com
            </a>
            </div>
 

         </div>


        <div class="mt-16">
           <div>
            <router-link to="/members"  class="select-none no-underline bg-gray-200 mb-4 p-2 inline-block rounded hover:bg-gray-300 border-gray-800 border-2 cursor-pointer text-gray-800" style=" text-shadow: 1px 1px #eee;"> View Revenue Sharing  </router-link> 
        </div>
        
         <div>
            <router-link to="/stake"  class="select-none no-underline bg-blue-700 mb-4 p-2 inline-block rounded hover:bg-blue-900 border-gray-800 border-2 cursor-pointer text-blue-100" style=" text-shadow: 1px 1px #222;"> Stake to Earn   </router-link> 
        </div>


          
        </div>



         </div>
        
          
        
       </div>
     </div>
   </div>


  


    
  <Footer/>

</div>
</template>


<script>



import Web3Plug from '../js/web3-plug.js'  

 
import FrontPageMedia from './components/FrontPageMedia.vue';
 
import Navbar from './components/Navbar.vue';
 
import Footer from './components/Footer.vue';
import TabsBar from './components/TabsBar.vue';
  
import StarflaskAPIHelper from '../js/starflask-api-helper.js';
import FrontendHelper from '../js/frontend-helper.js';


export default {
  name: 'Home',
  props: [],
  components: {Navbar, Footer, TabsBar, FrontPageMedia },
  data() {
    return {
      web3Plug: new Web3Plug() , 
      activePanelId: null, 
       

      tileItems: [ {
         url: 'https://market.onsecondary.com',
         imageName: 'OnSecondaryMarketPromo.png'
      }]
    }
  },

  created(){

 
    this.web3Plug.getPlugEventEmitter().on('stateChanged', function(connectionState) {
        console.log('stateChanged',connectionState);
         
        this.activeAccountAddress = connectionState.activeAccountAddress
        this.activeNetworkId = connectionState.activeNetworkId 
         
      }.bind(this));
   this.web3Plug.getPlugEventEmitter().on('error', function(errormessage) {
        console.error('error',errormessage);
         
        this.web3error = errormessage
       
      }.bind(this));

      this.web3Plug.reconnectWeb()
   
       

  },
  mounted: function () {
         
    
  }, 
  methods: {
          setActivePanel(panelId){
              if(panelId == this.activePanelId){
                this.activePanelId = null;
                return 
              }
               this.activePanelId = panelId ;
          },
          onTabSelect(tabname){
            console.log(tabname)

              this.selectedTab = tabname.toLowerCase()


          },

          getRouteTo(dest){
            return FrontendHelper.getRouteTo(dest)
          },

          getImgUrl(fileName){
               return require('../assets/images/'+fileName)
          }

       
 

  }
}
</script>
