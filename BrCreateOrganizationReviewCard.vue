<template>
  <div class="fit">
    <q-card>
      <q-card-title>
        <div class="q-headline">
          Summary
        </div>
      </q-card-title>
      <q-card-separator />
      <q-card-main>
        <div>
          <div class="q-title text-weight-light q-my-md">
            Business Information
          </div>
        </div>
        <div
          v-for="(val, key) in form.businessInfo"
          :key="key">
          <div class="uppercase text-bold q-mt-md q-mb-xs">
            {{val.label}}
          </div>
          <div
            v-if="key === 'corporateOfficer'"
            class="row justify-between items-center"
            style="width: 100%">
            <div>{{identityResolver(val.value)}}</div>
          </div>
          <div v-else>
            {{val.value}}
          </div>
        </div>
        <div
          class="q-my-md"
          style="width: 100%">
          <q-card-separator inset />
        </div>
        <div
          v-for="data in form.addressInfo"
          :key="data.label">
          <div class="uppercase text-bold q-mt-md q-mb-xs">
            {{data.label}}
          </div>
          <div>
            {{data.value}}
          </div>
        </div>
      </q-card-main>
    </q-card>
  </div>
</template>
<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

export default {
  name: 'BrCreateOrganizationReviewCard',
  props: {
    form: {
      type: Object,
      default: undefined,
      required: true
    },
    identityResolver: {
      type: Function,
      default: undefined,
      required: true
    }
  }
};
</script>
<style>
</style>
