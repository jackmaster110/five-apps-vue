<template>
  <div class="note">
    <h4>{{ this.title }}</h4>
    <span>{{ this.body }}</span>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component({
  components: {},
})
export default class App extends Vue {
  @Prop() title!: string;
  @Prop() body?: string;
}
</script>
