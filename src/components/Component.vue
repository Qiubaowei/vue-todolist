<template>
    <div style="width: 100px; margin-left: 43%;">
        <input v-model="newItem" v-on:keyup.enter="onEnter">
        <ul>
            <li v-for="item in items" v-bind:class="{finished: item.isfinish}" v-on:click="clickMe(item)">
              {{ item.label }}
            </li>
        </ul>
    </div>
</template>

<script>

export default {
    name: 'component',
    data: function () {
        return {
            newItem: '',
            items: []
        }
    },
    methods: {
        onEnter: function () {
            this.items.push({
                label: this.newItem,
                isfinish: false,
            });
            this.newItem = ""
        },
        clickMe: function (item) {
            item.isfinish = !item.isfinish;
            this.$http.get('http://localhost:3000/movies/movie').then(function(response){
            //this.$http.get('https://api.douban.com/v2/book/1220562').then(function(response){
                console.log(response)
            }, function(response){
                // 响应错误回调
                console.error(response)
            });

        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .finished{
      text-decoration: underline;
    }
</style>
