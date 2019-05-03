<template>
  <div class="fit">
    <div
      class="text-uppercase text-bold q-mt-md q-mb-xs">
      {{entry.label}}
    </div>
    <div v-if="entry.value.startsWith('#')">
      <q-chip
        square
        :style="{'background-color': entry.value}"
        text-color="white"
        class="q-my-none q-mx-none">
        {{entry.value}}
      </q-chip>
      <q-btn flat color="grey-10" icon="fas fa-eye-dropper" size="10px" class="q-pa-sm">
        <q-popup-proxy>
          <q-color v-model="entry.value" />
        </q-popup-proxy>
      </q-btn>
    </div>
    <div v-else>
      {{entry.value}}
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
    },
  }
};
</script>
<style>
</style>
