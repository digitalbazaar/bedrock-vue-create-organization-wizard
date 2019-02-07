<template>
  <q-page
    class="column gutter-md background"
    padding>
    <div class="column items-center">
      <br-create-organization-wizard />
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
    return {};
  }
};
</script>
<style>
</style>
