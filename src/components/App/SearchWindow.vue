<template>
    <div>
        <ion-toolbar>
            <ion-title>検索ページ</ion-title>
            <ion-buttons slot="start">
                <ion-back-button></ion-back-button>
            </ion-buttons>
        </ion-toolbar>
        <ion-searchbar animated :value="value" @change="value = $event.target.value, input()"></ion-searchbar>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                value: ""
            }
        },
        methods: {
            input(){
                this.$emit('input', this.value)
            }
        }
    }
</script>
<style scoped>
    ion-toolbar {
        --background: #BF0E00;
    }
    ion-searchbar {
        --background: #F3F3F3;
    }
    ion-title {
        --color: #ffffff;
    }
</style>
