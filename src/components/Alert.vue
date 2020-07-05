<template>
    <ion-vue-page>
        <ion-button @click="presentAlertConfirm">アラートが出るボタン！</ion-button>
        <div v-if="!notice">
            通知が許可されていません！
        </div>
        <div v-if="notice">
            通知が許可されました！
        </div>
    </ion-vue-page>
</template>

<script>
    export default {
        name: 'Alert',
        data () {
          return {
              notice: false
          }
        },
        methods: {
            presentAlertConfirm() {
                return this.$ionic.alertController
                    .create({
                        cssClass: 'my-custom-class',
                        header: '通知',
                        subHeader: '通知許可してくれたら嬉しい！',
                        message: 'このアプリに通知を許可しますか？',
                        buttons: [
                            {
                                text: 'キャンセル',
                                role: 'cancel',
                                cssClass: 'secondary',
                                handler: blah => {
                                    console.log('Confirm Cancel:', blah)
                                    this.notice = false
                                },
                            },
                            {
                                text: 'OK',
                                handler: () => {
                                    console.log('Confirm Okay')
                                    this.notice = true
                                },
                            },
                        ],
                    })
                    .then(a => a.present())
            },
        }
}
</script>
