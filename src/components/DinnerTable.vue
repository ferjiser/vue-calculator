<template>
<table>
        <tbody>
            <tr>
                <td>Dinner</td>
                <td>{{dinner | currency}}</td>
                <td>
                    <button @click="increment('dinner')">+</button>
                    <button @click="decrement('dinner')">-</button>
                </td>
            </tr>
            <tr>
                <td>Tip</td>
                <td>{{tip |currency}}</td>
                <td>
                    <button @click="increment('tip')">+</button>
                    <button @click="decrement('tip')">-</button>
                </td>
            </tr>
            <tr>
                <td>People</td>
                <td>{{people}}</td>
                <td>
                    <button @click="increment('people')">+</button>
                    <button @click="decrement('people')">-</button>
                </td>
            </tr>
            <tr>
                <td>Total with taxes ({{this.taxes}}%)</td>
                <td>{{totalWithTaxes | currency}} </td>
                <td></td>
            </tr>
            <tr>
                <td>Total with tip</td>
                <td>{{totalWithTips |currency}}</td>
                <td></td>
            </tr>
            <tr>
                <td>Total per person</td>
                <td>{{totalPerPerson | currency}}</td>
                <td></td>
            </tr>
        </tbody>
    </table>
</template>

<script>
const LOCAL_STORAGE_AMOUNTS_KEY = 'amounts';

export default {
  name: 'DinnerTable',
  data(){
      return {
        dinner: 0,
        tip: 0,
        people: 1,
        taxes: 21
      }
  },
  mounted(){
        const {dinner= this.dinner, tip=this.tip, people=this.people}  = JSON.parse(localStorage.getItem(LOCAL_STORAGE_AMOUNTS_KEY)) || {};
        this.dinner= dinner,
        this.tip= tip,
        this.people= people
    },
   computed: {
        totalWithTaxes() {
            return this.dinner*(1+this.taxes/100);
        },
        totalWithTips() {
            return this.totalWithTaxes + this.tip;
        },
        totalPerPerson() {
            return this.people > 0 ? this.totalWithTips/this.people: 0;
        },
        stateToLocalStorge(){
           return {
               dinner: this.dinner,
               people: this.people,
               tip: this.tip
           }
        }
    },
  filters: {
    currency(amount) {
        const CURRENCY = '€';
        return `${amount.toFixed(2)} ${CURRENCY}`;
    }
  },
  methods: {
        increment(type){
            this[type]++;
        },
        decrement(type){
            this[type] > 0 && this[type]--;
        }
    },
    watch: {
        stateToLocalStorge(){
            localStorage.setItem(LOCAL_STORAGE_AMOUNTS_KEY, JSON.stringify(this.stateToLocalStorge))
        }
    } 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
        table {
            margin: 25px auto;
            border-collapse: collapse;
            border: 1px solid #eee;
            border-bottom: 2px solid #42b883;
            box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.1),
                0px 10px 20px rgba(0, 0, 0, 0.05),
                0px 20px 20px rgba(0, 0, 0, 0.05),
                0px 30px 20px rgba(0, 0, 0, 0.05);
        }

        table tr:hover {
            background: #f4f4f4;
        }

        table tr:hover td {
            color: #555;
        }

        table td {
            color: #999;
            border: 1px solid #eee;
            padding: 12px 35px;
            border-collapse: collapse;
        }

        table tr td:nth-child(2) {
            text-align: right;
        }

        /* Buttons */

        button {
            padding: 4px 7px;
            border-radius: 1px;
            outline: none;
        }
</style>
