<template>
  <q-stepper
    ref="stepper"
    v-model="currentStep"
    class="fit no-shadow"
    contractable>
    <q-step
      v-for="(step, index) in steps"
      :key="index"
      default
      :name="index"
      :title="step.title">
      <div class="column justify-center items-center">
        <q-icon
          size="100px"
          :name="step.iconName"
          class="text-primary q-my-lg" />
        <h3 class="text-weight-light q-my-sm">
          {{step.label}}
        </h3>
        <h6
          v-if="step.sublabel"
          class="text-weight-light q-my-md">
          {{step.sublabel}}
        </h6>
        <div
          v-show="index > 0"
          class="fit"
          style="max-width: 600px;">
          <div class="q-mx-xl q-mb-xl">
            <br-organization-form
              v-if="index === 1"
              v-model="value.businessInfo" />
            <br-address-form
              v-else-if="index === 2"
              v-model="value.addressInfo" />
            <br-create-organization-review-card
              v-else
              :identity-resolver="identityResolver"
              :form="value" />
            <q-field v-if="index === 1">
              <q-select
                v-model="value.businessInfo.corporateOfficer.value"
                :float-label="value.businessInfo.corporateOfficer.label"
                filter
                :options="personas"
                class="q-pa-sm q-mt-md" />
            </q-field>
          </div>
        </div>
      </div>
    </q-step>
    <q-stepper-navigation class="absolute-bottom-right">
      <q-btn
        v-show="!firstStep"
        outline
        color="primary"
        size="md"
        label="Back"
        @click="previous()" />
      <q-btn
        v-if="!finalStep"
        class="q-ml-sm"
        color="primary"
        size="md"
        label="Next"
        @click="next()" />
      <q-btn
        v-else
        class="q-ml-sm"
        color="primary"
        size="md"
        label="Done"
        @click="done()" />
    </q-stepper-navigation>
  </q-stepper>
</template>
<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

import {BrAddressForm} from 'bedrock-vue-address-form';
import {BrOrganizationForm} from 'bedrock-vue-organization-form';
import BrCreateOrganizationReviewCard
  from './BrCreateOrganizationReviewCard.vue';

export default {
  name: 'BrCreateOrganizationWizard',
  components: {
    BrAddressForm,
    BrCreateOrganizationReviewCard,
    BrOrganizationForm
  },
  props: {
    value: {
      type: Object,
      default: undefined,
      required: true
    },
    personas: {
      type: Object,
      default: () => ([]),
      required: true
    },
    identityResolver: {
      type: Function,
      default: undefined,
      required: true
    }
  },
  data() {
    return {
      steps: [
        {
          iconName: 'fas fa-walking',
          label: 'Welcome, let\'s get started!',
          sublabel: 'We need to walk through a few steps to create an' +
                  ' Organization.',
          title: 'Introduction',
        },
        {
          iconName: 'far fa-list-alt',
          label: 'Let\'s fill out some information about your business',
          title: 'Business Information'
        },
        {
          iconName: 'fas fa-map-marker-alt',
          label: '...just a few more details on where you\'re located',
          title: 'Address Information'
        },
        {
          iconName: 'fas fa-check-circle',
          label: 'Does this look okay?',
          title: 'Review and Submit'
        }
      ],
      currentStep: 0
    };
  },
  computed: {
    firstStep() {
      return this.currentStep === 0;
    },
    finalStep() {
      return this.currentStep === this.steps.length - 1;
    }
  },
  created() {
    if(!this.value.businessInfo.corporateOfficer.label) {
      this.$emit('input', {
        ...this.value,
        businessInfo: {
          ...this.value.businessInfo,
          corporateOfficer: {
            ...this.value.businessInfo.corporateOfficer,
            label: 'Corporate Officer'
          }
        }
      });
    }
  },
  methods: {
    done() {
      this.$emit('done');
    },
    next() {
      this.$refs.stepper.next();
    },
    previous() {
      this.$refs.stepper.previous();
    }
  }};
</script>
<style>
</style>
