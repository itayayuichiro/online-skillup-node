<template>
    <div>
        <ul id="example-1">
            <li v-for="message in $props.messages">
                {{ message.text }}
            </li>
        </ul>
    </div>
</template>

<script>
import VueTypes from 'vue-types';

export default {
  props: {
    messages: VueTypes.isRequired
  }
};
</script>

<style lang="scss" scoped>
//
</style>
