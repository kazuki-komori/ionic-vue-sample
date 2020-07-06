<template>
    <div class="search">
        <ion-header>
            <ion-toolbar>
                <Search-window @input="input" />
            </ion-toolbar>
        </ion-header>
        <ion-content class="ion-padding">
            <Result :SearchVal='val'/>
        </ion-content>
    </div>
</template>
<script>
    import SearchWindow from '../../components/App/SearchWindow'
    import Result from '../../components/App/Result'
    export default {
        data(){
            return {
                val: ""
            }
        },
        components: {
            SearchWindow,
            Result
        },
        methods: {
          input(val) {
              this.val = val
          }
        }
    }
</script>
<style scoped>
    ion-toolbar {
        --background: #BF0E00;
    }
</style>
