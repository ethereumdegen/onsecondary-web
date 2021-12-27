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

            <div class="hidden text-white text-xl my-4">  Neutral grass-roots organization.  </div> 

     

           

        <div class="" style="">
        <div class=""  style="margin:0 auto;max-width:600px">
            <img src="@/assets/images/clubsos_v3.png" class="pl-4" />
        </div>
         </div>


        <div class="mt-16">
           <div>
            <router-link to="/members"  class="select-none no-underline bg-gray-200 mb-4 p-2 inline-block rounded hover:bg-gray-300 border-gray-800 border-2 cursor-pointer text-gray-800" style=" text-shadow: 1px 1px #eee;"> View Members  </router-link> 
        </div>
        
         <div>
            <router-link to="/stake"  class="select-none no-underline bg-blue-700 mb-4 p-2 inline-block rounded hover:bg-blue-900 border-gray-800 border-2 cursor-pointer text-blue-100" style=" text-shadow: 1px 1px #222;"> Stake to Earn   </router-link> 
        </div>


          <div>
            <router-link to="/contribute"  class="select-none no-underline bg-gray-200 mb-4 p-2 inline-block rounded hover:bg-gray-300 border-gray-800 border-2 cursor-pointer text-gray-800" style=" text-shadow: 1px 1px #eee;"> Market your Dapps with Club SOS  </router-link> 
        </div>
        </div>



         </div>
        
          
        
       </div>
     </div>
   </div>


    <div class="section  text-white  border-b-2 border-black " style="background:#222;">
     <div class="w-container  ">

         

          <div class=" w-2/3  mt-8 py-8" style="margin: 0 auto;">
           
                <div class="text-2xl text-center"> How It Works </div>

                

                <ul class=" "> 
                    <li class="my-4"> 1. Stake SOS in the Club SOS Contract </li>
                    <li class="my-4" > 2. Web3 applications donate some of their income to the Contract as revenue-share to use as a marketing+branding boost to all SOS holders </li>
                    <li class="my-4" > 3. Unstake SOS at any time to withdraw <span class="text-purple-300"> your original deposit + accrued donations </span>  </li>
               </ul>

                <div class="text-lg text-center my-16  "> TLDR: This is donations router for community-driven marketing and incentivization. </div>


                <p class="text-gray-500 bg-gray-800 p-4 mt-8"> <img src="@/assets/images/information.png" width="20" class="inline"/> Services perform revenue-share to the Club contract to incentivize SOS holders to participate and market their application since this gives SOS holders a financial interest in the application's success. </p>

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
          }

       
 

  }
}
</script>
