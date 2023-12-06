<template>
    <header>
        <div class="center">
            <button v-on:click="foo()">Answer</button>
            <p v-if="visible">I'm just fine, {{ title }}, thanks for asking.</p>
            <div v-background>Lorem ipsum</div>
            <div v-background:green>Lorem ipsum</div>
        </div>
    </header>
</template>

<script lang="ts">
    // DO NOT USE <script setup>

    //vue options API.
    /*
    import { defineComponent } from "vue";
    export default defineComponent({});
    */

    //class component

    import { Component, Vue, toNative } from 'vue-facing-decorator'
    @Component
    class TheWelcome extends Vue {
        title: string = 'normie'
        visible = false

        foo(): void {
            this.visible = !this.visible
            this.title = 'homie'
        }
    }
    export default toNative(TheWelcome)
</script>

<style>
    /* header .center {
        display: flex;
        place-items: center;
    } */

    @media (min-width: 1024px) {
        header {
            display: flex;
            place-items: center;
            padding-right: calc(var(--section-gap) / 2);
        }

        header .wrapper {
            display: flex;
            place-items: flex-start;
            flex-wrap: wrap;
        }
    }
</style>
