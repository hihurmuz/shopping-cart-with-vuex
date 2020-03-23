<template>
    <div id="products">
        <h2>Products</h2>
        <div class="notification" v-for="(info,key) in infos" :key="key">
            {{info}}
        </div>
        <table :class="{products : products.length !==0}">
            <tr>
                <th>Product Name</th>
                <th>Price</th>
                <th>Buy</th>
            </tr>
            <tr v-for="product in products" :key="product.id">
                <td>{{product.name}}</td>
                <td>{{product.price}}</td>
                <td>
                    <label>
                        <input type="number" :id="product.id" value="0">
                    </label>
                </td>
                <td>
                    <button @click="addToCard(product)">Add to card</button>
                </td>
            </tr>
        </table>
    </div>
</template>
<script>
    import { mapState } from 'vuex';
export default {
    data(){
        return{
            infos:[]
        }
    },
    computed:{
        ...mapState(['products'])
    },
    methods:{
        addToCard(product){
            if (document.getElementById(product.id).value > 1){
                const count = document.getElementById(product.id).value;
                product={...product,count};
                this.$store.commit('addToCard',product);
                const info =product.name +'  added to card';
                this.infos.push(info);
                setTimeout(()=>{
                    document.getElementById(product.id).value =0;
                    this.infos.splice(this.infos.indexOf(info),1);
                },3000)
            }else {
                const info ='please enter a valid input';
                this.infos.push(info);
                setTimeout(()=>{
                    document.getElementById(product.id).value =0;
                    this.infos.splice(this.infos.indexOf(info),1);
                },3000)
            }
        }
    }
}
</script>

<style>
    #products{
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .products {
        border: 1px solid #ddd;
        margin: auto;
    }

    .products td,
    th {
        border: 1px solid #ddd;
        padding: 10px;

    }

    .notification {
        background-color: #ddd;
        padding: 20px;
        width: 400px;
        margin-bottom: 20px;
        border-radius: 25px;
        font-size: 24px;
    }

    button {
        border: none;
        cursor: pointer;
        padding: 5px 10px;
    }
</style>