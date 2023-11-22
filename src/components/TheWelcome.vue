<template>
    <h1>hello</h1>
    <p v-if="visible">Maintenant vous me voyez {{title}}</p>
    <button v-on:click="foo()">ok</button>
  </template>
  <script lang="ts">
  // DO NOT USE <script setup>
  
  //vue options API.
  /*
  import { defineComponent } from "vue";
  export default defineComponent({});
  */
  
  //class component

  import { Component, Vue, toNative } from "vue-facing-decorator";
  @Component
  class TheWelcome extends Vue {

        title: string = 'test'
        visible = true;

        foo():void{
            this.visible = !this.visible
            this.title = 'test1'
        }

  }
  export default toNative(TheWelcome)
  </script>
  <style>
  </style>