<template>
  <div class="fit">
    <br-wizard
      :current-step-index="stepIndex"
      :total-steps="steps.length"
      @back="back($event)"
      @finish="done($event)"
      @next="next($event)"
      @index="stepIndex = $event">
      <br-wizard-step
        :heading="currentStep.heading"
        :image="currentStep.image"
        :icon="currentStep.icon"
        :subheading="currentStep.subheading">
        <div class="q-pb-xl full-width">
          <br-organization-form
            v-if="steps[stepIndex].name === 'Organization Information'"
            v-model="value.businessInfo">
            <q-select
              v-model="value.businessInfo.corporateOfficer.value"
              :label="value.businessInfo.corporateOfficer.label"
              :options="personas"
              emit-value
              map-options
              class="q-pa-sm q-mt-md" />
          </br-organization-form>
          <br-address-form
            v-if="steps[stepIndex].name === 'Address Information'"
            v-model="value.addressInfo" />
          <br-create-organization-review-card
            v-if="steps[stepIndex].name === 'Review and Submit'"
            :identity-resolver="identityResolver"
            :form="value" />
        </div>
      </br-wizard-step>
    </br-wizard>
  </div>
</template>
<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

import {BrAddressForm} from 'bedrock-vue-address-form';
import {BrOrganizationForm} from 'bedrock-vue-organization-form';
import {BrWizard, BrWizardStep} from 'bedrock-vue-wizard';
import BrCreateOrganizationReviewCard
  from './BrCreateOrganizationReviewCard.vue';

export default {
  name: 'BrCreateOrganizationWizard',
  components: {
    BrAddressForm,
    BrCreateOrganizationReviewCard,
    BrOrganizationForm,
    BrWizard,
    BrWizardStep
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
      stepIndex: 0,
      steps: [
        {
          icon: {
            name: 'fas fa-walking',
            size: '65px',
            color: 'primary'
          },
          heading: 'Welcome, let\'s get started!',
          subheading: 'We need to walk through a few steps to create an' +
                  ' Organization.',
          name: 'Introduction'
        },
        {
          icon: {
            name: 'far fa-list-alt',
            size: '65px',
            color: 'primary'
          },
          heading: 'Let\'s fill out some information about your business',
          name: 'Organization Information'
        },
        {
          icon: {
            name: 'fas fa-map-marker-alt',
            size: '65px',
            color: 'primary'
          },
          heading: 'Where are you located?',
          name: 'Address Information'
        },
        {
          icon: {
            name: 'fas fa-check-circle',
            size: '65px',
            color: 'primary'
          },
          heading: 'Does this look okay?',
          name: 'Review and Submit'
        }
      ]
    };
  },
  computed: {
    currentStep() {
      return this.steps[this.stepIndex];
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
          },
          color: {
            ...this.value.businessInfo.color,
            label: 'Profile Color'
          }
        }
      });
    }
  },
  methods: {
    back(event) {
      this.$emit('back', event);
    },
    done(event) {
      this.$emit('done', event);
    },
    next(event) {
      this.$emit('next', event);
    }
  }
};
</script>
<style>
</style>
