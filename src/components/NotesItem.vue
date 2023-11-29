<template>
    <div class="notes__item">
        {{note.id}}
        <div class="notes__item-top">
            <h2 class="notes__item-title">{{note.title}}</h2>
            <p class="notes__item-date">{{note.date}}</p>
        </div>
        <p class="notes__item-text">{{note.text}} </p>
        <div class="notes__item-buttons">
            <button class="notes__item-btn edit" @click="$emit('changeNote', note)">
                <img src="@/assets/images/pen.svg" alt="">
                <span>{{ $t ("editwindowbtn") }}</span>
            </button>
            <button class="notes__item-btn del" @click="$emit('delNote', note.id)">
                <img src="@/assets/images/delete.svg" alt="">
                <span>{{  $t ("deledit") }}</span>
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        props:{
            note:Object
        }
    }
</script>

<style lang="scss" scoped>

</style>