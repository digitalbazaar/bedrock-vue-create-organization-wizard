<template>
  <q-page
    class="column gutter-md background"
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
          entityType: {
            value: ''
          },
          corporateOfficer: {
            value: ''
          }
        },
        addressInfo: {
          addressLocality: {
            value: ''
          },
          addressRegion: {
            value: ''
          },
          postalCode: {
            value: ''
          },
          streetAddress: {
            value: ''
          }
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
    done() {
      console.log('Done!', this.form);
    },
    identityResolver(id) {
      const persona = this.personas.filter(({value}) => value === id)[0];
      return persona ? persona.label : 'n/a';
    }
  }
};
</script>
<style>
</style>
