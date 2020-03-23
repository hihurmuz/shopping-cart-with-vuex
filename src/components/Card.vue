<template>
    <div>
        <h2>Card</h2>
        <ul>
            <li v-for="item in card" :key="item.id">
            <span class="item-name">
                {{item.name}}
                <button @click="deductItemCount(item)">-1</button>
                <button @click="removeItem">X</button>
            </span>
                <span class="item-count">{{item.count}} X{{item.price}}</span>
                <span class="item-amount">{{formatCurrency(item.count*item.price)}}</span>
            </li>
        </ul>
        <div v-if="card.length ===0 ">
            <h2>No item </h2>
        </div>
        <div v-else>
            <div class="total-amount">Total: {{formatCurrency(totalAmount)}}</div>
            <button @click="clearAll">Clear All</button>
            <button>CheckOut</button>
        </div>
    </div>
</template>

<script>
import {mapState,mapMutations,mapGetters} from 'vuex';
export default {
    computed:{
        ...mapState(['card']),
        ...mapGetters(['totalAmount'])
    },
    methods:{
        formatCurrency(price){
            return '$'+price.toFixed(2)
        },
        ...mapMutations(['deductItemCount','removeItem','clearAll'])
    }

}
</script>
<style>
    ul {
        list-style: none;
    }

    li {
        display: flex;
        max-width: 700px;
        margin: 10px auto auto;
    }

    .item-name {
        text-align: left;
        font-size: 18px;
        flex: 2;
    }

    .item-count {
        font-size: 25px;
        margin-left: 10px;
        flex: 2;
    }

    .item-amount {
        text-align: left;
        flex: 1;
    }

    .total-amount {
        border-top: 2px solid #333;
        border-bottom: 2px solid #333;
        padding: 10px 20% 10px 10px;
        margin: 10px;
        font-size: 29px;
        text-align: right;
    }

    button {
        border: none;
        cursor: pointer;
        padding: 5px 10px;
    }
</style>