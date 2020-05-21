<template>
  <component
    :is="!isStatic && isInternal(to) ? 'nuxt-link' : 'a'"
    class="cta"
    :href="to"
    :to="!isStatic && isInternal(to) ? to : null"
    :rel="isExternal(to) ? 'noopener' : null"
    :target="isExternal(to) ? '_blank' : null"
    v-on="$listeners"
  >
    <slot />
  </component>
</template>

<script lang="ts">
import Vue from 'vue'
import { Component, Prop } from 'vue-property-decorator'

@Component
export default class extends Vue {
  @Prop(String) to
  @Prop(Boolean) isStatic

  isExternal (url: string): boolean {
    return url.startsWith('http')
  }

  isMail (url: string): boolean {
    return url.startsWith('mailto')
  }

  isInternal (url: string): boolean {
    return !(this.isExternal(url) || this.isMail(url))
  }
}
</script>

<style lang="scss" scoped>
@import '~carbon-components/scss/globals/scss/typography';

.cta {
  display: inline-block;
  text-decoration: none;
  border: 2px solid;

  @include type-style('productive-heading-02');
  padding: $spacing-04 $spacing-05;
  border-color: $interactive-01;
  text-transform: uppercase;
  white-space: nowrap;
  color: $text-01;
  background-color: $ui-01;

  fill: currentColor;
}
</style>