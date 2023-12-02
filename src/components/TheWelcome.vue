<template>
  <div class="home">
    <h1>How are you?</h1>
    <p v-if="visible">I'm just fine, {{ title }}, thanks for asking.</p>
    <button v-on:click="foo()">answer</button>
    <div v-background>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</div>
    <div v-background:green>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</div>
  </div>
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
  title: string = 'not cool person'
  visible = false

  foo(): void {
    this.visible = !this.visible
    this.title = 'homie'
  }
}
export default toNative(TheWelcome)
</script>
<style></style>
