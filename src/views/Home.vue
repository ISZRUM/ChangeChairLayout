<template lang='pug'>
v-layout#Home(fill-height column)
    .main-pane
        template
            v-container(fluid)
                v-card-title 教卓
                v-layout(justify-center fill-height column xs12 md12)
                    v-flex
                        v-layout(row wrap)
                            v-dialog(v-model='dialog' presistent max-width='600px')
                                template(v-slot:activator='{ on }')
                                    v-btn.card-style.ma-2(v-on='on' v-for='i in $store.state.className' :key='i')
                                        h1.center(xs2 md2) {{ i.num }}
                                //- dialog card information
                                v-card
                                    v-card-title
                                        span.headline Chair Information
                                    v-card-text
                                        v-container(grid-list-md)
                                            v-layout(wrap)
                                                v-flex(xs12 sm8 md8)
                                                    v-text-field(label='First name')
                                                v-flex(xs12 sm4 md4)
                                                    v-text-field(label='Attendance number' required)
                                        v-card-actions
                                            v-spacer
                                            v-btn(color='blue darken-1' flat @click='dialogInfo') Save
                                            v-btn(color='blue darken-1' flat @click='dialogInfo') Close

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
    protected dialog = false;
    protected text = '';
    protected max = 43;
    protected async dialogInfo() {
        this.dialog = false;
        return 33;
    }
}
</script>

<style lang='stylus'>
@require '~@/assets/styles/entry/_view.styl';

html
    scroll-view: true;
    // static-view: true;

#Home
    .main-pane
        main-pane();
    .center
        text-align :center;
    .card-style
        width :14%;
        min-width : 10%;
        height :4rem;
</style>
