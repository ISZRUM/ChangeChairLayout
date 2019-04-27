<template lang='pug'>
v-layout#Home(fill-height column)
    .main-pane
        template
            v-container(fluid)
                v-layout(align-start justify-start fill-height column xs12 md12)
                v-card-title.center 教卓
                    v-flex
                        v-layout(row wrap justify-center)
                            v-card.card-style.ma-2(v-for='i in 43' :key='i' xs2 md2)
                                h1.center {{ i }}
        //- v-btn(@click='onClick' v-for='i in nameList' :key='i') {{ i.num }}
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
    // protected wait = 'false';
    // protected chair: number[] = new Array(43);
    // protected async onClick() {
    //     for (let i = 1; i in this.nameList ; i++) {
    //         for (let j = 1 ; j <= i ; j++) {
    //             if ( this.nameList[j].jage !== 0 )　{
    //                 this.chair[i] = Math.floor(Math.random() * this.nameList.length);
    //                 this.nameList[this.chair[i]].jage = 1;
    //                 break;
    //             }
    //         }
    //     }
    // }
    // protected newLine()  {
    //     for (let i = 1; i <= 43; i++) {
    //         return i;
    //     }
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
        height :3rem;
</style>
