<template>
    <div class="notes container">
        <div class="notes__top">
            <h2 class="notes__title">
                {{ notes.length == 0 ? $t("noinfobar") : $t("infobar")}}
            </h2>
            <button class="notes__button" @click="grid = !grid">
                <img src="@/assets/images/list.svg" alt="" v-if="grid">
                <img src="@/assets/images/grid.svg" alt="" v-else>
                <span>{{grid ? $t("list") : $t("grid")}}</span>
            </button>
        </div>
        <div class="notes__list" :class="{active: !grid}">
            <NotesItem @changeNote="$emit('changeNote', $event)" @delNote="$emit('delNote', $event)" v-for="(note, index) in notes" :key="index" :note="note"/>
        </div>
    </div>
</template>

<script>
import NotesItem from '@/components/NotesItem.vue'
    export default {
        data(){
            return {
                grid:true
            }
        },
        components:{
            NotesItem
        },
        props:{
            notes:Array
        }
    }
</script>

<style lang="scss" scoped>

</style>