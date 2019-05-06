<template lang='pug'>
v-layout#Home(fill-height column)
    .main-pane
        template
            v-container(fluid)
                v-card.ma-3.pa-1
                    v-layout(justify-center)
                        v-card.orange.lighten-3.ma-2(width='15vw' :aspect-ratio='9/16')
                            v-card-text 教卓
                    v-layout(justify-center column)
                        v-flex
                            v-layout(row wrap align-center justify-space-around)
                                v-dialog(v-model='dialog' presistent max-width='600px')
                                    template(v-slot:activator='{ on }')
                                        v-card.primary.lighten-4.mb-2(v-for='member in 43' :key='member' v-on='on' width='calc(100vw/7.5)' :aspect-ratio='1' @click='onClick(member)')
                                            v-card-text(canter) {{ member }}
                                    //- dialog card information
                                    v-card
                                        v-card-title
                                            span.headline Chair Information
                                        v-card-text
                                            v-container(grid-list-md)
                                                v-layout(wrap)
                                                    v-flex(xs12 sm8 md8)
                                                        v-text-field(label='First name' v-model='hoge.name')
                                                    v-flex(xs12 sm4 md4)
                                                        v-text-field(label='Attendance number' v-model='hoge.an' required)
                                            v-card-actions
                                                v-spacer
                                                v-btn(color='blue darken-1' flat @click='false') Save
                                                v-btn(color='blue darken-1' flat @click='false') Close

    p hoge {{this.hoge}}
    //- p huga {{this.huga}}
    p member {{this.member}}

</template>

<script lang='ts'>
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from '@/components/HelloWorld.vue';

@Component({
    components: {
        HelloWorld,
    },
})
export default class Home extends Vue {

    protected hoge = 0;
    protected huga = 0;
    protected an = 0 ;
    protected dialog = false;
    protected text = '';

    protected onClick(member: number) {
        this.hoge = member;
    }
    protected change(member: number, hoge: number) {
        this.huga = hoge;
        hoge = member;
        member = this.huga;
        this.dialog = false;
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
