<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h3 class="text-center my-3">Invoice Maker</h3>
        <form action="" @submit.prevent="saveRecord">
          <div class="row">
            <div class="col-6">
              <select name="" id="" class="form-select" v-model="selectedService">
                <option value="">Select Service</option>
                <option  v-for="service in services"  :value="service.id" :key="service.id">
                  {{service.name}}
                </option>
              </select>
            </div>
            <div class="col-4">
              <input type="number" v-model="inputQuantity" class="form-control">
            </div>
            <div class="col-2">
              <button class="btn btn-primary w-100">
                <i class="fa-solid fa-plus"></i>
              </button>
            </div>
          </div>
        </form>
        <table class="table table-bordered mt-3">
          <thead>
          <tr>
            <th>#</th>
            <th>Service</th>
            <th>UnitPrice</th>
            <th>Quantity</th>
            <th>Cost</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="record in records" :key="record.id">
              <td>
                {{record.id}}
                <span><i class=""></i></span>
              </td>
            <td>{{record.service.name}}</td>
            <td class="text-end">{{record.service.price}}</td>
            <td class="text-end">{{record.quantity}}</td>
            <td class="text-end">{{record.cost}}</td>
          </tr>
          </tbody>
          <tr>
            <td v-if="records.length == 0" colspan="5" class="text-center">No Record</td>
          </tr>
          <tfoot>
          <tr v-if="records.length > 0">
            <td colspan="4">Total</td>
            <td class="text-end">{{records.reduce((pv,cv)=>pv+cv.cost,0)}}</td>
          </tr>
          </tfoot>
        </table>
        <div class="row g-2 mt-3">
          <div class="col-6">
            <input v-model="invoiceId" class="form-control">
          </div>
          <div class="col">
            <button class="btn btn-primary" @click="toPrint">
              <i class="fa-solid fa-print">Print</i>
            </button>
          </div>
          <div class="col">
            <button class="btn btn-primary" @click="toPrint">
              <i class="fa-solid fa-print">Save</i>
            </button>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedService : null,
      inputQuantity : null,
      invoiceId : '',
      services : [
        {
          id : 1,
          name : 'WebDesign',
          price : 100
        } ,
        {
          id : 2,
          name : 'Domain',
          price : 10
        } ,
        {
          id : 3,
          name : 'SSl',
          price : 10
        } ,
        {
          id : 4,
          name : 'Maintain',
          price : 5
        } ,
      ],
      recordId :1,
      records : []
    }
  },
  computed: {
    invoiceNumber() {
      let d = new Date();
      let dateCode = d.getDate()+""+(d.getMonth()+1)+""+d.getFullYear()
      let random = Math.floor(Math.random()*10000)
      return dateCode+"-"+random
    }
  },
  methods: {

    saveRecord() {
      let currentService = this.services.find(service=>service.id=== this.selectedService);
      let cost = currentService.price*this.inputQuantity;
      let record = {
        id : this.recordId,
        service : currentService,
        quantity : this.inputQuantity,
        cost
      }
      this.records.push(record);
      this.selectedService = this.inputQuantity = ""
      this.recordId++
    },
    del(){

    },
    toPrint(){
      print()
    }
  },

}
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.min.css";
@import "~@fortawesome/fontawesome-free";
@import "~animate.css/animate.min.css";
@media print{
  .hide-in-print{
    display: none;
  }
}
</style>