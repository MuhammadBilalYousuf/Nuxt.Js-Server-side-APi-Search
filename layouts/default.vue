<template>
<div>
    <Products :products="products" @set-filters="load($event)"/>
</div>
</template>

<script>
import Products from '../components/Products.vue'

export default {
   name: "backend",
   components: { Products },
    data(){
        return {
            products: [],
            filters: {
                s: ''
            }
        }
   },
   async mounted(){
       await this.load(this.filters);
   },
    methods: {
       async load(f){
           this.filters.s = f.s;
           const arr = [];

           if(this.filters.s){
               arr.push(`s=${this.filters.s}`);
           }

            const response = await fetch(`http://localhost:8000/api/products/backend?${arr.join('&')}`);
            const content = await response.json();
            this.products = content.data;
            
       }
   }
}
</script>
