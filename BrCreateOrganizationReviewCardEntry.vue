<template>
  <div class="fit">
    <div
      class="text-uppercase text-bold q-mt-md q-mb-xs">
      {{label}}
    </div>
    <div>
      {{value}}
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
    label: {
      type: String,
      default: undefined,
      required: true
    },
    value: {
      type: String,
      default: undefined,
      required: true
    }
  }
};
</script>
<style>
</style>
