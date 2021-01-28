<template>
    <div class="main">
        <div class="header">
           <input type="text" v-model="title"> 
        </div>
        <div class="cascading-dropdown">
            <div class="dropdown">
                <span>If user is:</span>
                <select v-model="selectedStatus">
                    <option value="">Choose Status</option>
                    <option v-for="(country_obj, status, index) in options" v-bind:key= index :value="status">{{status}}</option>
                </select>
            </div>
            <div class="dropdown">
                <span>.then</span>
                <select :disabled="action.length == 0" v-model="selectedAction">
                    <option value="">Choose Action</option>
                    <option v-for="(time_obj, time, index) in action" v-bind:key= index>{{time}}</option>
                </select>
            </div>
            <div class="dropdown">
                <span></span>
                <select :disabled="time.length == 0" v-model="selectedTime">
                    <option value="">Choose when</option>
                    <option v-for="(t, index) in time" v-bind:key= index >{{t}}</option>
                </select>
            </div>
        </div>
        <Button  :onClick="createUserRule"/>
    </div>
</template>

<script>
import Button from './Button.vue';
import { EventBus } from '../main.js';

export default {
    name: 'CreateRule',
    components: {
        Button
    },
   data: function() {
  return {
    title: 'Untitled rule',
    ruleCase: 'If user is',
    options: {
                "Active": {
                    "Anonymize": ["1", "2", "3", "4"],
                    "Deactivate": ["After X Days", "User's first day", "User's last day"],
                    "Delete": ["4", "5", "6", "7"],
                },
                "Anonymous": {},
                "Created": {},
                "Deactivated": {},
    },
            action: [],
            time: [],
            selectedStatus: "",
            selectedAction: "",
            selectedTime: ""
      }
   },
   methods: {
      createUserRule() {
        console.log('createRule');
        EventBus.$emit('CreateRuleEvent', (this.title));
     }
   },
   watch: {
           selectedStatus: function() {
            // Clear previously selected values
            this.action = [];
            this.time = [];
            this.selectedAction = "";
            this.selectedTime = "";
            // Populate list of actions in the second dropdown
            if (this.selectedStatus.length > 0) {
                this.action = this.options[this.selectedStatus]
            }
        },
            selectedAction: function() {
            // Clear previously selected values
            this.time = [];
            this.selectedTime = "";
            console.log(this.selectedAction);
            // Now we have a status and action. Populate list of time in the third dropdown
            if (this.selectedAction.length > 0) {
                this.time = this.options[this.selectedStatus][this.selectedAction];
                console.log(this.time);
            }
        }
   }
}

</script>
<style scoped lang="scss">
@import "../styles/main.scss";

.main {
  width: 90%;
  height: 200px;
  box-sizing: border-box;
  background: #ffffff;
  -webkit-box-shadow: 2px 0px 4px 0px rgba(0,0,0,0.75);
  -moz-box-shadow: 2px 0px 4px 0px rgba(0,0,0,0.75);
  box-shadow: 2px 0px 4px 0px rgba(0,0,0,0.75);
  padding: 10px;
  display: flex;
  margin: 0 auto;
  border-radius: 10px;
  
.header {
    font-size: $font-primary-bold;
    font-weight: 600;
    margin-bottom: 15px;
    input { 
      border: none;
      &:focus {
        outline: 0 !important;
        border: none !important;
      }
   }
}

.cascading-dropdown {
  display: flex;
  flex-direction: row;
  .dropdown {
    margin: 10px 4px;
    span {
      margin-right: 5px;
    }
  }
}

  .button {
    background: #808080;
  }
}
</style>