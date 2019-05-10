<template lang='pug'>
v-layout#Home(fill-height column)
    .main-pane
        template
            v-container(fluid)
                v-card.ma-3.pa-1
                    v-layout(justify-center)
                        v-dialog(v-model='dialog' presistent max-width='600px')
                            template(v-slot:activator='{ on }')
                                v-card.orange.lighten-3.ma-2(v-on='on' width='15vw' :aspect-ratio='9/16')
                                    v-card-text 教卓
                            //- dialog card information
                            v-card
                                v-card-title
                                    span.headline Chair Information
                                v-card-text
                                    v-container(grid-list-md)
                                        v-layout(wrap)
                                            v-flex(xs12 sm12 md12)
                                                v-text-field(label='出席番号' v-model='res_anum')
                                            v-flex(xs12 sm12 md12)
                                                v-text-field(label='position-number' v-model='res_pos' required)
                                            v-flex(xs12 sm12 md12)
                                                v-text-field(label='password' v-model='msg.mask' required) {{ maskMsg() }}
                                            v-card-actions(xs12 sm8 md6)
                                                v-btn(color='blue darken-1' flat @click='onSend') Send
                                            v-card-actions(xs12 sm4 md6)
                                                v-btn(color='blue darken-1' flat @click='false') Cancel
                    v-layout(justify-center column)
                        v-flex
                            v-layout(row wrap align-center justify-space-around)
                                //- v-dialog(v-model='dialog' presistent max-width='600px')
                                //-     template(v-slot:activator='{ on }')
                                v-card.primary.lighten-4.mb-2(v-for='i in num' :key='i' width='calc(100vw/7.5)' :aspect-ratio='1')
                                    v-card-text(canter) {{ i }}

</template>

<script lang='ts'>
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from '@/components/HelloWorld.vue';
import io from 'socket.io-client';

@Component({
    components: {
    },
})
export default class Home extends Vue {

    protected dialog = false;
    protected num = [] as string[];
    protected socket = io();
    protected res_anum = 0;
    protected res_pos = 0;
    protected res_pass = '';
    // protected res_name = '';
    protected msg = {
        mask: '',
    };
    // 初期状態
    protected created() {
        for (let i = 0; i < 43; i++) {
            this.num[i] = String(i + 1);
        }
        this.socket.on('all_seats' , (seats: string) => {
            console.log(seats);
            const jseats = JSON.parse(seats);
            for (const seat of jseats) {
                this.insertNum(seat.name, seat.position);
            }
        });
        this.socket.on('new_seat', (seat: string) => {
            console.log(seat);
            const jseats = JSON.parse(seat);
            this.insertNum(jseats.name, parseInt(jseats.position, 10));
            console.log(jseats.position);
            typeof(jseats.position);
        });
    }

    protected onSend() {
        if (this.res_anum === 0 || this.res_pos === 0 || this.res_pass === '') {
            return;
        }

        const myJson = {
            id: this.res_anum,  // attendance number
            position: this.res_pos,
            passward: this.res_pass,
            // name: this,res_name,
        };

        this.socket.emit('res_seat', JSON.stringify(myJson));
        // let a = this.insertNum(myJson.id, myJson.position);
        // console.log(myJson);
        // console.log(a);
        [ this.res_pass, this.msg.mask ] = ['' , ''];
        this.res_anum = 0;
        this.res_pos = 0;
        this.dialog = false;    // dialogを閉じる
    }

    protected insertNum(name: string, pos: number ) {
        this.num[pos] = name;
        this.num.push();
        // console.log(this.num[pos]);
    }

    protected maskMsg() {
        const char = this.msg.mask.charAt(this.msg.mask.length - 1);

        // 複数回呼ばれるため一文字に対して一回だけ
        if (char !== '*') {
            this.res_pass += char;   // 末尾にマスク前の文字列を追加
            this.msg.mask = this.msg.mask.replace(/\S/g, '*');  // 全ての文字を置き換える
            // console.log(this.res_pass);
        }
    }
}
</script>

<style lang='stylus'>
@require '~@/assets/styles/entry/_view.styl';

html
    scroll-view: true;
    // static-view: true;

#Homeh
    .main-pane
        main-pane();
    .center
        text-align :center;
    .card-style
        // width :14%;
        // min-width : 10%;
        height :4rem;
</style>
