<template>
  <q-page
    class="column q-col-gutter-md background"
    padding>
    <div class="row items-center">
      <br-create-organization-wizard
        v-model="form"
        :personas="personas"
        :identity-resolver="identityResolver"
        @done="done" />
    </div>
  </q-page>
</template>
<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

import {BrCreateOrganizationWizard} from
  'bedrock-vue-create-organization-wizard';
import {randomColor} from 'randomcolor';

export default {
  name: 'Home',
  components: {BrCreateOrganizationWizard},
  data() {
    return {
      form: {
        businessInfo: {
          legalName: {
            value: ''
          },
          color: {
            value: randomColor()
          },
          entityType: {
            value: ''
          },
          corporateOfficer: {
            value: ''
          }
        },
        addressInfo: {
          addressCountry: '',
          addressLocality: '',
          addressRegion: '',
          postalCode: '',
          streetAddress: ''
        }
      },
      personas: [
        {
          label: 'Persona 1',
          value: '0001'
        },
        {
          label: 'Persona 2',
          value: '0002'
        },
        {
          label: 'Persona 3',
          value: '0003'
        }
      ]
    };
  },
  methods: {
    async done(event) {
      const {waitUntil} = event;
      const p = sleep(2000);
      await waitUntil(p);
      console.log('Done!', this.form);
    },
    identityResolver(id) {
      const persona = this.personas.filter(({value}) => value === id)[0];
      return persona ? persona.label : 'n/a';
    }
  }
};

function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
</script>
<style>
</style>
