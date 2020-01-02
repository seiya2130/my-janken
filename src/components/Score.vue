<template>
    <div id="score">
        <h2>せいせき</h2>
        <div><button class="button" type="button" @click="resetScore">クリア</button></div>
        <ul v-if="scores">
             <li v-for="(score, index) in scores" :key="index"><span>{{ index + 1 }}回目：</span>{{ score.msg }}</li>
        </ul>
    </div>
</template>
<script>
export default {
    name: 'score',
    props: { 
        'scores': {
            type: Array,
            required: true
        },
        'resetScore': {
            type: Function,
            requrred: true
        }
    },
    data() {
        return {}
    }
}
</script>
<style scoped>
    /* CSS省略 */
    /* @import "../style/style.css"; */
   
   
</style>