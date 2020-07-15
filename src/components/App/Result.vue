<template>
    <div>
        <ion-button expand="block" @click="search(SearchVal)" id="top">検索</ion-button>
        <div v-if="valid.blank" class="valid">
<!--            検索ボックスが空欄の時-->
            検索ボックスに何か入力してください。
        </div>
        <div v-if="valid.error" class="valid">
<!--            API系で何かしらのエラーが吐かれた時-->
            {{valid.message}}
        </div>
        <div v-if="data.length !== 0">
            <div v-for="(val, idx) in data" :key="idx">
                <ion-card>
                    <img :src="val.image" width="100"/>
                    <ion-card-header>
                        <ion-card-subtitle>
                            <span class="cardName">
                                {{val.name}}
                            </span>
                        </ion-card-subtitle>
                        <ion-card-title>
                            <span class="cardPrice">
                                {{val.price}}円
                            </span>
                        </ion-card-title>
                    </ion-card-header>
                </ion-card>
            </div>
        </div>
    </div>
</template>
<script>
    import axios from 'axios'

    export default {
        props: {
            SearchVal: {
                type: String,
                default: '',
                required: false
            },
        },
        data(){
            return{
                data: [],
                valid: {
                    error: false,
                    blank: false,
                    message: ''
                }
            }
        },
        methods: {
            async search(val){
                this.valid.blank = false
                this.valid.error = false
                //ローダーを作動
                await this.onload()
                if (val === ''){
                    this.valid.blank = true
                    this.valid.error = true
                    this.offload()
                        .catch((e) => {
                            this.valid.error = true
                            this.valid.message = e
                        })
                }
                if (!this.valid.error){
                    try {
                        const searchVal = encodeURI(val)
                        const URL = `${process.env.VUE_APP_RAKUTEN_API_URL}&keyword=${searchVal}&hits=15&applicationId=${process.env.VUE_APP_APP_ID}`
                        const {data} = await axios.get(URL)
                        this.data = this.editData(data)
                        await true
                        //ローダーを停止
                        this.offload()
                    } catch (e) {
                        this.offload()
                        this.valid.error = true
                        this.valid.message = e
                    }
                }
            },
            editData(data){
                const res = []
                for (let element of data.Items){
                    let obj = {
                        name: '',
                        price: '',
                        image: ''
                    }
                    obj.name = element.Item.itemName
                    obj.price = element.Item.itemPrice
                    obj.image = element.Item.mediumImageUrls[0]?.imageUrl ?? ''
                    res.push(obj)
                }
                return res
            },
            onload(){
                return this.$ionic.loadingController
                    .create({
                        cssClass: 'my-custom-class',
                        message: '更新中...',
                    })
                    .then(loading => {
                        return loading.present()
                    })
            },
            offload(){
                return this.$ionic.loadingController.dismiss()
            }
        }
    }
</script>
<style scoped>
    .cardPrice{
        font-size: 30px;
    }
    .cardName{
        font-size: 20px;
    }
    ion-card-title{
        --color: red;
    }
    .valid{
        color: red;
    }
</style>
