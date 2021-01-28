<template>
  <div class="main">
    <div class="rule-info" v-if="!isActiveRule">
   <div class="header">User Automation</div>
   <div class="subheader" >
     <p>Now you can create automations and automatically perform actions in regards to your users.</p>
     <p>You can decide when users should be <strong>activated</strong>, <strong>dezactived</strong>, <strong>anonymized</strong> and <strong>deleted</strong>.
     </p>
     </div>
     <Button :onClick="createUserRule"/>
    </div>
     <CreateRule v-if="isActiveRule"/>
     <Rules v-if="isActiveRule"/>
  </div>
</template>

<script>
import Button from './Button.vue';
import CreateRule from './CreateRule.vue';
import Rules from './Rules.vue';

export default {
  name: 'User',
  components: {
    Button,
    CreateRule,
    Rules
  },
  data: () =>({
    isActiveRule: false
  }),
  methods: {
    createUserRule() {
      this.isActiveRule = true;
    }
  }
}
</script>

<style scoped lang="scss">
@import "../styles/main.scss";

.main {
  display: flex;
  flex-direction: column;
  font-size:  $font-primary-size;
  position: relative;
  top: 100px;
  
  .rule-info {
    display: flex;
    flex-direction: column;
  }

  .header {
    font-size: $font-primary-bold;
    font-weight: 600;
    margin: 0 auto;
  }
  .subheader {
    margin: 0 auto;
  }
}
</style>
