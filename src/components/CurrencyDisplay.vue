<template>
    <div class="currency-display">
        <div class="input-group mb-3">
            <div class="input-group-prepend">
            <span v-html="data.code + ' ' + data.symbol" class="input-group-text"></span>
            </div>
            <input v-bind:value="formatValue" v-bind:readonly="true" type="text" class="form-control" v-bind:placeholder="data.description" aria-label="Username" aria-describedby="basic-addon1">
            <div class="pl-2">
            <a href="#">
                <font-awesome-icon v-on:click.prevent="updateDisplayValue(false)" size="2x" icon="times-circle" />
            </a>
            </div>
        </div>
    </div>
</template>

<script>
export default {

    name: "CurrencyDisplay",
    props: {
        amount: String,
        data:{
            display: Boolean,
            code: String,
            symbol: String,
            rate_float: Number,
            amount: String,
            description: String
        }
    },
    methods: {
       updateDisplayValue: function(displayValue)  {
            this.$emit('display', {currency: this.data.code, displayValue: displayValue});
        }  
    },
    computed: {
        formatValue: function() {
            let calculated = this.data.rate_float * this.amount;
            return calculated != 0 ? calculated.toFixed(2).replace(/(\d)(?=(\d{3})+(?:\.\d+)?$)/g, "$1,") : ""
        } 
    }
};
</script>