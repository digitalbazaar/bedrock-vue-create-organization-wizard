<template>
  <div class="fit">
    <div
      class="text-uppercase text-bold q-mt-md q-mb-xs">
      {{entry.label}}
    </div>
    <div>
      <slot name="color">
        {{entry.value}}
      </slot>
    </div>
  </div>
</template>
<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

export default {
  name: 'BrCreateOrganizationReviewCardEntry',
  props: {
    entry: {
      type: Object,
      default: undefined,
      required: true
    }
  }
};
</script>
<style>
</style>
