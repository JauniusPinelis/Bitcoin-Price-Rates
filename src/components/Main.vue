<template>
  <div class="main">
  
    <section class="program-name">
      <div class="container">
        <div class="row">
          <div class="col text-center py-5">
            <h1 class="display-5">Bitcoin Price Rates</h1>
          </div>
        </div>
      </div>
    </section>
  
    <section class="main">
      <div class="container">
        <div class="row">
          <div class="col-md-6">
            <div class="input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text">BTC ₿</span>
              </div>
              <input v-model="input" type="number" class="form-control" placeholder="Bitcoins">
              <div class="input-group-append">
                <b-dropdown variant="info" v-show="displayAddCurrenciesDropdown" text="Add a currency">
                  <b-dropdown-item v-for="currency in data" v-bind:key="currency.code" v-show="!currency.display" v-html="currency.description + ' - ' + currency.code" v-on:click="currency.display = true">
                  </b-dropdown-item>
                </b-dropdown>
              </div>
            </div>
          </div>
          <div class="col-md-6">
            <currency-display v-for="currency in data" v-show="currency.display" v-on:display="updateDisplayValue($event)" v-bind:key="currency.code" v-bind:data="currency" v-bind:amount="input">
            </currency-display>
          </div>
        </div>
      </div>
    </section>
  
  </div>
</template>

<script>
  import axios from "axios";
  
  export default {
    name: "Main",
    data: () => ({
      data: [],
      input: null,
      timer: ''
    }),
    computed: {
      displayAddCurrenciesDropdown: function() {
        return !this.data.every(o => o.display == true)
      },
    },
    methods: {
      updateDisplayValue(event) {
        var currency = this.data.find(obj => {
          return obj.code == event.currency
        });
        currency.display = event.displayValue;
      },
      fetchData(notify) {
        var self = this;
        axios
          .get("https://api.coindesk.com/v1/bpi/currentprice.json")
          .then(response => {
  
            self.tempData = [];
  
            Object.keys(response.data.bpi).forEach((currencyName) => {
              var dataObject = response.data.bpi[currencyName];
  
              //Tracking which currencies are displayed/hidden
              if (self.data.length != 0) {
                var currency = self.data.find(obj => {
                  return obj.code == dataObject.code
                });
                dataObject.display = currency.display;
              }
              else{
                dataObject.display = 1;
              }

              self.tempData.push(dataObject);
            });
  
            self.data = self.tempData;
  
            if (notify) {
              this.displayUpdateLabel();
            }
          })
          .catch(e => {
            this.displayError();
          });
      },
      displayUpdateLabel() {
        this.$notify({
          group: 'notification',
          title: '',
          text: 'Currency rates have been updated'
        })
      },
      displayError() {
        this.$notify({
          group: 'notification',
          title: '',
          type: 'error',
          text: 'Something wrong has happened'
        })
      },
      updateData(){
        this.fetchData(true)
      }
    },
    created() {
      this.fetchData(false);
      // Updates every 60 seconds
      this.timer = setInterval(this.updateData, 60000)
    },
    beforeDestroy() {
      clearInterval(this.timer)
    }
  };
</script>
