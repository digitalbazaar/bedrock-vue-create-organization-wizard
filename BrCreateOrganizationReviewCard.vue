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
          v-for="entry in businessInfoEntries"
          :key="entry">
          <br-create-organization-review-card-entry
            :entry="entry">
            <template #color v-if="entry.value.startsWith('#')">
              <q-chip
                square
                :style="{'background-color': form.businessInfo.color.value}"
                text-color="white"
                class="q-my-none q-mx-none">
                {{form.businessInfo.color.value}}
              </q-chip>
              <q-btn
                flat
                color="grey-10"
                icon="fas fa-eye-dropper"
                size="10px"
                class="q-pa-sm">
                <q-popup-proxy>
                  <q-color v-model="form.businessInfo.color.value" />
                </q-popup-proxy>
              </q-btn>
            </template>
          </br-create-organization-review-card-entry>
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
      const {businessInfo} = this;
      return [
        {
          label: 'Legal Name',
          value: businessInfo.legalName.value
        },
        {
          label: 'Entity Type',
          value: businessInfo.entityType.value
        },
        {
          label: 'Corporate Officer',
          value: await this.identityResolver(
            businessInfo.corporateOfficer.value)
        },
        {
          label: 'Profile Color',
          value: businessInfo.color.value
        }
      ];
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
    },
    businessInfo() {
      return this.form.businessInfo;
    }
  }
};
</script>
<style>
</style>
