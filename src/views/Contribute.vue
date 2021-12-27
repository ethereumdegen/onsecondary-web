<template>

<div>

   <div class="section  bg-gray-200  border-b-2 border-black px-0 lg:px-1">

     <div class=" ">
        <Navbar 
        v-bind:web3Plug="web3Plug" 
       />
     </div>


   </div>

  

   <div class="section   border-b-2 border-black text-black" style="background:#eee;">
     <div class="py-16 w-container">
        
       <div class="w-column">
           
         

          <div  class=""  >
  
                
              <div class="text-xl text-center">
                Supercharge  marketing for your application!
              </div>
              <div class="text-sm text-center hidden">
                 
              </div> 
             </div>

               <div class="mt-4" style="">
        <div class=""  style="margin:0 auto;max-width:600px">
            <img src="@/assets/images/clubsos_v4.png" class="pl-4" />
        </div>
         </div>


              <div  class=" flex flex-col lg:flex-row  mt-16"  >

                    <div class="p-4 bg-gray-300">
                      <div class="ul ">
                        <div class="li my-4">
                        - Buy SOS with some of the revenue that your application generates and donate the SOS to the Club SOS contract!  It will be split equally amongst all stakers.
                            </div> 

                             <div class="li my-4">
                        - This is done by transferring SOS tokens directly to 0xf14f78349882254e4d52cf24d9c5d3fd219d68c0.
                            </div> 

                        <div class="li my-4">
                        - All SOS holders are now financially incentivized to promote your project. Let them know that you are revenue sharing to them via Club SOS!  They just need to stake their SOS in the Club SOS contract to start earning risk-free revenue share from your project. 
                        </div> 
                       
                            
                      </div> <!-- ul --> 
                    </div> 
              
               </div> 
          
           </div>
     </div>
   </div>


    


    
  <Footer/>

</div>
</template>


<script>



import NotConnectedToWeb3 from './components/NotConnectedToWeb3.vue'

import Web3Plug from '../js/web3-plug.js'  

 

import Navbar from './components/Navbar.vue';
 
import Footer from './components/Footer.vue';
import TabsBar from './components/TabsBar.vue';
import GenericTable from './components/GenericTable.vue';
 

import MathHelper from '../js/math-helper.js'

import StarflaskAPIHelper from '../js/starflask-api-helper.js'

import FrontendHelper from '../js/frontend-helper.js'

export default {
  name: 'Contribute',
  props: [],
  components: {Navbar, Footer, TabsBar, GenericTable, NotConnectedToWeb3},
  data() {
    return {
      web3Plug: new Web3Plug() 
     
       
    
    }
  },

  created(){

 
    this.web3Plug.getPlugEventEmitter().on('stateChanged', async function(connectionState) {
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
         
  }
}
</script>
