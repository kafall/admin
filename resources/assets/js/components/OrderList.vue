<template>
    <div class="w-full">
   <!--  <div v-if="this.success!=null" class="alert alert-success text-white" id="success-alert">{{this.success}}</div> -->
       
    <div class="flex items-center justify-between pt-2 pb-4 border-b" style="border-color: 1px solid #f3f3f3;">
    <h2 class="text-base text-gray-700 font-semibold">Order</h2>
  
    </div>
       
       
       
      
 <div class="my-3">
      <div class="flex flex-col lg:flex-row lg:items-center lg:justify-between search_sec pt-3">
        <div class="">  <div class="mb-0">
          <div class="flex items-center">
          <div>
      <div class="relative sort_by">
        <select v-on:change="getOrder()" v-model="sort_by" class="block appearance-none w-32 lg:w-40  border custom_border py-1 px-4 pr-8 rounded-full  focus:outline-none focus:bg-white focus:outline-none text-xs" id="grid-state">
       
          <option value="asc">Ascending</option>
          <option value="desc">Descending</option>
        </select>
        <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 ">
          <svg class="fill-current h-4 w-4 select_icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
        </div>
      </div>
   
          </div>
          <div class="relative mx-3">
            <input type="text" v-on:change="getOrder()" v-model="search" placeholder="Search" class="text-xs border custom_border rounded-full  py-1 focus:outline-none px-4 w-32 lg:w-40">
            <img src="images/icons_1/search.svg" class="w-3 h-3 absolute top-0 right-0 m-2">
          </div>
          </div>
          </div>
        </div>
        <div class="flex items-center mt-3 lg:mt-0">
          <p class="text-xs custom_txt mx-2">1-5 of 20</p>
           <div class="relative sort_by">
        <select  v-on:change="getOrder()" v-model="selectpaginate" class="block appearance-none   border custom_border py-1 px-2 pr-5 rounded-full  focus:outline-none focus:bg-white focus:outline-none text-xs" id="grid-state">
           
          <option  value="10">10</option>
          <option value="15">15</option>
        </select>
        <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 ">
          <svg class="fill-current h-4 w-4 select_icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
        </div>
      </div>
        </div>
      </div>
    </div>

    <div class="seller_table bg-white">
    <div class="my-5 overflow-y-auto">
      <table class="w-full">
        <thead>
          <tr> 
            <th>orderno</th>
            <th>address</th>
            <th>shippingmethod</th>
            <th>paymentmethod</th>
            <th>subtotal</th>
            <th>status</th>
            <th>Action</th>
          </tr>
        </thead>
      <tbody>
      <tr v-for="order in list"  class="seller_list rounded  bg-white">
      
      <td class="px-3 py-3">
          <div class="flex items-center ">
            {{order.orderno}}
        </div>
        
      </td>

      <td class="px-3 py-3">
          <div class="flex items-center ">
            {{order.address}}
        </div>
        
      </td>

      <td class="px-3 py-3">
          <div class="flex items-center ">
             {{order.shippingmethod}}
        </div>
        
      </td>

      <td class="px-3 py-3">
          <div class="flex items-center ">
              {{order.paymentmethod}}
        </div>
        
      </td>

      <td class="px-3 py-3">
          <div class="flex items-center ">
             {{order.subtotal}}
        </div>
        
      </td>

      <td class="px-3 py-3">
          <div class="flex items-center ">
         
          {{order.status}}
        </div>
        
      </td>

      
      <td class="px-3 py-3">
        <ul class="list-reset flex items-center action_icon"> 

<li>
  <a v-on:click="showPopup(order.status,order.id)" href="#">
  <svg class="fill-current w-4 h-4 mx-2" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 383.947 383.947" style="enable-background:new 0 0 383.947 383.947;" xml:space="preserve" width="512px" height="512px"><g><g>
  <g>
    <g>
      <polygon points="0,303.947 0,383.947 80,383.947 316.053,147.893 236.053,67.893    " data-original="#000000" class="active-path" fill=""/>
      <path d="M377.707,56.053L327.893,6.24c-8.32-8.32-21.867-8.32-30.187,0l-39.04,39.04l80,80l39.04-39.04     C386.027,77.92,386.027,64.373,377.707,56.053z" data-original="#000000" class="active-path" fill=""/>
    </g>
  </g>
</g></g> </svg></a>
</li>
<!-- <li>
  <a v-on:click="orderDelete(order.id)" href="#">
    <svg class="fill-current w-4 h-4" xmlns="http://www.w3.org/2000/svg" height="512px" viewBox="-47 0 512 512" width="512px"><g><path d="m416.875 114.441406-11.304688-33.886718c-4.304687-12.90625-16.339843-21.578126-29.941406-21.578126h-95.011718v-30.933593c0-15.460938-12.570313-28.042969-28.027344-28.042969h-87.007813c-15.453125 0-28.027343 12.582031-28.027343 28.042969v30.933593h-95.007813c-13.605469 0-25.640625 8.671876-29.945313 21.578126l-11.304687 33.886718c-2.574219 7.714844-1.2695312 16.257813 3.484375 22.855469 4.753906 6.597656 12.445312 10.539063 20.578125 10.539063h11.816406l26.007813 321.605468c1.933594 23.863282 22.183594 42.558594 46.109375 42.558594h204.863281c23.921875 0 44.175781-18.695312 46.105469-42.5625l26.007812-321.601562h6.542969c8.132812 0 15.824219-3.941407 20.578125-10.535157 4.753906-6.597656 6.058594-15.144531 3.484375-22.859375zm-249.320312-84.441406h83.0625v28.976562h-83.0625zm162.804687 437.019531c-.679687 8.402344-7.796875 14.980469-16.203125 14.980469h-204.863281c-8.40625 0-15.523438-6.578125-16.203125-14.980469l-25.816406-319.183593h288.898437zm-298.566406-349.183593 9.269531-27.789063c.210938-.640625.808594-1.070313 1.484375-1.070313h333.082031c.675782 0 1.269532.429688 1.484375 1.070313l9.269531 27.789063zm0 0" data-original="#000000" class="active-path" fill=""/><path d="m282.515625 465.957031c.265625.015625.527344.019531.792969.019531 7.925781 0 14.550781-6.210937 14.964844-14.21875l14.085937-270.398437c.429687-8.273437-5.929687-15.332031-14.199219-15.761719-8.292968-.441406-15.328125 5.925782-15.761718 14.199219l-14.082032 270.398437c-.429687 8.273438 5.925782 15.332032 14.199219 15.761719zm0 0" data-original="#000000" class="active-path" fill=""/><path d="m120.566406 451.792969c.4375 7.996093 7.054688 14.183593 14.964844 14.183593.273438 0 .554688-.007812.832031-.023437 8.269531-.449219 14.609375-7.519531 14.160157-15.792969l-14.753907-270.398437c-.449219-8.273438-7.519531-14.613281-15.792969-14.160157-8.269531.449219-14.609374 7.519532-14.160156 15.792969zm0 0" data-original="#000000" class="active-path" fill=""/><path d="m209.253906 465.976562c8.285156 0 15-6.714843 15-15v-270.398437c0-8.285156-6.714844-15-15-15s-15 6.714844-15 15v270.398437c0 8.285157 6.714844 15 15 15zm0 0" data-original="#000000" class="active-path" fill=""/></g> </svg>

  </a>
</li>
 -->
        </ul>
      </td>
      </tr>
       

      </tbody>
      </table>
    </div>
    
    </div>









<!-- popup -->

 
 <div v-bind:class="[this.popup==1?'block':'hidden']">   
 <div class="modal-mask">
   <div class="modal-wrapper px-4">
     <div class="modal-container w-full  max-w-md  mx-auto">
       <div class="modal-body">
        
             
            <div class="modal-header flex justify-between items-center border-b px-4 py-1">

                 <h2 class="text-sm font-semibold">Status Update</h2>
             <button class="modal-default-button text-2xl py-1"  id="close_modal" v-on:click="closePopup()">
                &times;
            </button>
                       
          </div>    
           
               <div class="py-6 px-4">
              <label class="form-group block my-1 custom-label text-sm">Select Status</label>
          <select v-model="selectStatus" v-on:change="confirm()" class="border text-sm px-2 py-1 w-full mb-2">
            
               <option v-for="status in statusList" :value="status" >{{status}}</option>
               
          </select>
          </div>
        </div>
      </div>
    </div>
</div>

</div>
<div v-if="list.length==0">
  <p>No Records</p>
</div>

<div class="custom-paginate py-2">
 <paginate
    v-model="page"
    :page-count="this.page_count"
    :page-range="3"
    :margin-pages="1"
    :click-handler="getOrder"
    :prev-text="'<'"
    :next-text="'>'"
    :container-class="'pagination'"
    :page-class="'page-item'"
    :prev-link-class="'prev'"
    :next-link-class="'next'">
  </paginate>
</div>
  </div>    
</template>

<script>

var Paginate = require('vuejs-paginate')
Vue.component('paginate', Paginate)
import Vue from 'vue'
import VueSwal from 'vue-swal'    

    export default {
         props:['orderlist'],
     
        data(){
            return {
               page_count:0,
                page:0,
                total :'',
                 statusList:['pending','processing','payment_failed','shipped','completed','refunded','hold','cancel'],
          
                  
                 id:'',
                 paginate_arr:['10','15'],
                 list:[],
                 errors:[],
                 success:null,
                 sort_by:'asc',
                 selectpaginate:'10',
                 popup:0,
                 search:'',
            }
        },
        created() {
           // alert(this.orderlist);
           this.getOrder();
        },
      methods:{
        getOrder(page =1)
        {
          // alert(this.selectpaginate);

          axios.post('/admin/order/getdata/'+this.orderlist+'?&page='+page,{
              sort_by:this.sort_by,
              search:this.search,
              paginate:this.selectpaginate,
             }).then(response=>{
              this.list=response.data.data;
              // console.log('hi');
              // console.log(this.list);
              this.page_count = response.data.meta.last_page;
              this.total = response.data.meta.total;

                console.log(this.list);
           });
        },

        
    //   orderDelete(id)
    //   {
    //      swal({

    //           title: "Are you sure?",
    //           icon: "warning",
    //           buttons: true,
    //           dangerMode: true,
    //      })
    //    .then((willdelete) => {
    //          if (willdelete) {
        
    //                success:null;
    //                 errors:[];
    //                 //alert(id);
    //                 axios.get('/admin/order/'+id+'/destroy').then(response=>{
    //                   this.success=response.data.messages;
    //               //    console.log(this.success);
    //                   this.getOrder();

    //       });
           
    //           swal("Deleted!", {
    //               icon: "success",
    //              });
               
               
    //          }
    //           else {
    //                swal("Order Deleted is cancel!");
    //          }
    //    });


    // },

   

      closePopup()
      {
         this.popup=0;
         this.selectStatus='';
         this.id='';
      },

      showPopup(status,id)
      {
                 
         this.popup=1;
         this.selectStatus=status;
         this.id=id;
         //alert(id);
      },
             

      // getOrder(page=1)
      // {

      //     axios.get('/admin/order/getpending?page=' + page).then(response=>{
      //         //this.list=response.data.data;
      //         this.list=response.data.data;
      //         this.page_count = response.meta.last_page;
      //         this.total = response.meta.total;
      //       //console.log(this.total);
      //      });
      // },
        confirm()
        {
          //this.status=status;
          
     swal({
      title: "Are you sure?",
      icon: "warning",
      buttons: true,
      dangerMode: true,
    })
    .then((willupdate) => {
      if (willupdate) {
          // alert(this.orderstatus);
          this.statusUpdate();
          
          
        swal("Status updated successfully!", {
          icon: "success",
        });


      } else {
        swal("Status update is cancel!");
      }
    });
        },

        statusUpdate(){
          this.success=null;
          this.errors=[];
          axios.post('/admin/order/'+this.id+'/statusupdate',{
            status:this.selectStatus,
            oldstatus:this.orderstatus,
          }).then(response=>{
              this.success=response.data.messages;
               // this.lists=response.data.data;
                //this.page_count = response.data.meta.last_page;
                //console.log(response);
                 this.getOrder();
              
          }).catch(error=>{
              this.errors=error.response.errors;
          });

         console.log('gfdfd');

        }
      },
    }
</script>

 
<style scoped>

.disp-none {
  display:none;
}
​
​
@media(max-width:640px){
  .modal-wrapper {
    width: 100% !important;
    left: 0 !important;
  }
}

.modal-container {
  margin: 0px auto;
 /* padding: 15px 15px;*/
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
}
​
.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}
​
.modal-body {
  margin: 20px 0;
}
​
.modal-default-button {
  float: right;
}
​
/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */
​
.modal-enter {
  opacity: 0;
}
​
.modal-leave-active {
  opacity: 0;
}
​
.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
.darktheme .modal-container {
    background: #1c1c1c;
    border: 1px solid #fff;
}
.darktheme .modal-wrapper {
    color: #fff;
}
.lighttheme .modal-wrapper{
    color: #000;
}
@media(max-width: 850px){
  .modal-body .flex.flex-m {
    flex-direction: column;
  }
  .modal-body .flex-m {
    align-items: normal;
  }
  .modal-header h2 {
    font-size: 20px;
  }
}
.trn-trade {
     color: #0275d8 !important;
    cursor: pointer;
    text-decoration: underline !important;
}
.trn-trade:hover {
  color: #0275d8 !important;
  text-decoration: underline !important;
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  transition: opacity 0.3s ease;
}
.modal-wrapper {
  vertical-align: middle;
  width: 34%;   
    left: 34%;
    position: absolute;
    right: 0;
    top: 25%;
    bottom: 0;
}
.alert-success {
/*  background-color: #7dc855;*/
  color: #7dc855;
}
/*psk-end*/
</style>