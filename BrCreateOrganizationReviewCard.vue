<template>
  <div class="fit">
    <q-card>
      <q-card-section>
        <div class="text-h5">
          Summary
        </div>
      </q-card-section>
      <q-separator />
      <q-card-section>
        <div>
          <div class="q-title text-weight-light q-my-md">
            Business Information
          </div>
        </div>
        <div
          v-for="entry in form.businessInfo"
          :key="entry">
          <br-create-organization-review-card-entry
            :identity-resolver="identityResolver"
            :entry="entry" />
        </div>
        <div
          class="q-my-md"
          style="width: 100%">
          <q-separator inset />
        </div>
        <div
          v-for="entry in addressInfoEntries"
          :key="entry">
          <br-create-organization-review-card-entry
            :entry="entry" />
        </div>
      </q-card-section>
    </q-card>
  </div>
</template>
<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

import BrCreateOrganizationReviewCardEntry from
  './BrCreateOrganizationReviewCardEntry.vue';

export default {
  name: 'BrCreateOrganizationReviewCard',
  components: {
    BrCreateOrganizationReviewCardEntry
  },
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
  },
  computed: {
    addressInfo() {
      return this.form.addressInfo;
    },
    addressInfoEntries() {
      const {addressInfo} = this;
      return [
        {
          label: 'Street Address',
          value: addressInfo.streetAddress
        },
        {
          label: 'City',
          value: addressInfo.addressLocality
        },
        {
          label: 'State/Province/Region',
          value: addressInfo.addressRegion
        },
        {
          label: 'ZIP/Postal Code',
          value: addressInfo.postalCode
        },
        {
          label: 'Country',
          value: addressInfo.addressCountry
        }
      ];
    }
  }
};
</script>
<style>
</style>
