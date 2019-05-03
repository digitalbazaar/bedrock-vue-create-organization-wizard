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
  asyncComputed: {
    async businessInfoEntries() {
      return [
        {
          label: 'Legal Name',
          value: this.form.businessInfo.legalName.value
        },
        {
          label: 'Entity Type',
          value: this.form.businessInfo.entityType.value
        },
        {
          label: 'Corporate Officer',
          value: await this.identityResolver(
            this.form.businessInfo.corporateOfficer.value)
        },
        {
          label: 'Profile Color',
          value: this.form.businessInfo.color.value
        },
      ];
    }
  },
  created() {
    console.log('Form', this.form);
  },
  computed: {
    addressInfoEntries() {
      return [
        {
          label: 'Street Address',
          value: this.form.addressInfo.streetAddress
        },
        {
          label: 'City',
          value: this.form.addressInfo.addressLocality
        },
        {
          label: 'State/Province/Region',
          value: this.form.addressInfo.addressRegion
        },
        {
          label: 'ZIP/Postal Code',
          value: this.form.addressInfo.postalCode
        },
        {
          label: 'Country',
          value: this.form.addressInfo.addressCountry
        }
      ];
    }
  }
};
</script>
<style>
</style>
