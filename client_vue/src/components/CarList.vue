<template>
        <div>
          <table class="table">
            <tr v-for="car in  filters"  >
              <td>
                <router-link  :to="'/carItem/'+car.id">
                  <img alt="car" class="car-img"  :src="car.img" @click="autoInfo(car.id)"/>
                </router-link>
              </td>
              <td>{{ car.brand }}</td>
              <td>{{ car.model }}</td>
            </tr>
          </table>
        </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'carList',
  props: ['isFilter'],
  data () {
    return {
      config: {
          headers: {'Content-Type': 'application/x-www-form-urlencoded'}
      },
      cars:{},
      //filter_cars: {},
      err_year: "",
      err_work: "",
      err_param:"",
      error_str : "We apologize, we have temporary problems with the service. return to us later"
  }
},
  created(){					
        if (localStorage['filter_cars']) {
          this.cars =  JSON.parse(localStorage['filter_cars'])
        }
  },
   computed:{
      filters(){
        var filterList = this.cars
        if(this.isFilter || !this.filter){
           if (localStorage['filter_cars']) {
          filterList =  JSON.parse(localStorage['filter_cars'])
        }
        }
       return filterList
      }
   },
  methods: {
    autoInfo(car_id){
            //this.clearError()
            //this.clearFilter()
            this.$parent.$options.methods.clearFilter();
            //this.shortInfoCars = false
            //this.fullInfoCar = true
            var self = this
            /*
            myAjax.post("client.php","getCarInfo[car_id] = "+ car_id,
                function(dataCar){
                    var data = JSON.parse(dataCar)
                    if( data['sucess']== "1"){
                        self.carItem.info  = data['info']
                        self.carItem.colors  = data['colors']
                        self.fullInfoCarRedirect = true
                    }else{
                        if(data['error']!=""){
                           self.err_param = data['error']
                           self.is_not_err_param = false;
                       } else{
                        self.err_work = error_str
                         self.is_not_err_work = false;
                        }
                       
                    }
            });
            */
        },
        
  
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.centr{
	text-align:center;
}

.car-img{
   max-height:100px;
   max-width:100px;
   cursor:pointer;
}

.bold{
    font-weight: bold;
}

.panel_table td{
    text-align: left;
}


.left{
    text-align:left;
}

.add_bag_btn{
	background-color : black;
	color: white;
  width: 100%;
}

</style>
