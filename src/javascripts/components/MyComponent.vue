<template>
    <div>
        <div>
            <div class="col-sm-3 col-sm-offset-4 frame">
                <ul>
                    <li v-for="message in $props.messages">
                        <div v-if="message.name == user_name">
                            <div class="msj-rta macro">
                                <div class="text text-l">
                                    <p>
                                        {{ message.name }}
                                    </p>
                                    <p>
                                        {{ message.text }}
                                    </p>
                                </div>
                            </div>
                        </div>
                        <div v-else>
                            <div class="msj macro">
                                <div class="text text-l">
                                    <p>
                                        {{ message.name }}
                                    </p>
                                    <p>
                                        {{ message.text }}
                                    </p>
                                </div>
                            </div>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>

    <!--<div>-->
        <!--<ul id="example-1">-->
            <!--<li v-for="message in $props.messages">-->
                <!--{{ message.text }}-->
            <!--</li>-->
        <!--</ul>-->
    <!--</div>-->
</template>

<script>
import VueTypes from 'vue-types';

export default {
  props: {
    messages: VueTypes.isRequired,
    user_name: ''
  }
};
</script>

<style lang="scss" scoped>
//
</style>
