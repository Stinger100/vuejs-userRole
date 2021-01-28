<template>
<div class="main">
<div class="header">
  <p>{{ title }}</p>
  <p>{{ activity }}</p>
</div>
<table>
        <tr>
			<th align="left"><input type="checkbox" v-model="selectAll" @click="select"></th>
            <th align="left">Rule Name</th>
        </tr>
        <tr v-for="rule in rules" v-bind:key="rule.id">
            <td>
                <input type="checkbox" v-model="selected" :value="rule.id" number @click="showCrudOperations(rule.id)">
            </td>
            <td>{{ rule.name }}</td>
			<div class="table-content">
			<div class="onoffswitch">
    <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" id="myonoffswitch" tabindex="0" checked>
    <label class="onoffswitch-label" for="myonoffswitch">
        <span class="onoffswitch-inner"></span>
        <span class="onoffswitch-switch"></span>
    </label>
	</div>
	<div class="test" @click="showCrudOperations(rule.id)"></div>
	</div>
	<div class="crud-options" v-if="selectedRuleId === rule.id">
		<p @click="deleteRule(rule.id)">Delete rule</p>
		<p>Edit rule</p>
	</div>
        </tr>
    </table>
</div>
</template>

<script>
import { EventBus } from '../main.js';

export default {
    name: 'Rules',
    data: () => ({
		selectedRuleId: 0,
		title: 'Rule Overview',
		ruleTitle: '',
		activity: 'Activity Log',
		rules: [
            { id: 1, name: "Dezactivate people on the last day", email: "pfeffer.matt@yahoo.com" },
            { id: 2, name: "Anonymize three months after deactivated", email: "mohammad.ferry@yahoo.com" },
            { id: 3, name: "Delete users one year after anonymized", email: "evolkman@hotmail.com" },
        ],
		selected: [],
		selectAll: false
	}),
	created() {
		EventBus.$on('CreateRuleEvent', (title) => {
		this.title = title;
		this.rules.push( {id: this.rules.length + 1, name: this.title, email:''});
		console.log(this.rules);
		});
	},
	methods: {
		select() {
			this.selected = [];
			if (!this.selectAll) {
				for (let rule in this.rules) {
					this.selected.push(this.rules[rule].id);
				}
			}
		},
		showCrudOperations(item) {
			if (this.selectedRuleId === item) {
				this.selectedRuleId = 0;
			} else {
			this.selectedRuleId = item;
			}
		},
		deleteRule(item) {
			this.rules = this.rules.filter((rule) => {
			return	rule.id !== item;
			});
		}
	}
}
</script>
<style scoped lang="scss">
.main {
    margin-top: 50px;
    width: 90%;
    height: 200px;
    padding: 10px;
	margin: 40px auto;
    .header {
		display: flex;
		margin-left: 15px;
        p {
			margin-right: 20px;
		&:first-child {
			color: #2F329F;
			}
        }
    }
	table {
		-webkit-box-shadow: 2px 0px 4px 0px rgba(0,0,0,0.75);
		-moz-box-shadow: 2px 0px 4px 0px rgba(0,0,0,0.75);
		border-collapse: collapse;
		background: #ffffff;
		border-radius: 5px;

	th, td {
		border-bottom: 1px solid grey;
		padding: 10px;
	}
	
	.crud-options {
		position: absolute;
		padding: 5px;
		top: 30%;
		right: 1%;
		border-radius: 5px;
		background: #3445C2;
		color: #ffffff;
		p {
			cursor: pointer;
		}
	}

	.table-content {
		display: flex;
		justify-content: space-evenly;
	.test:after {
		content: '\2807';
		font-size: 20px;
		cursor: pointer;
 }
	.onoffswitch {
	position: relative; 
	width: 60px;
    -webkit-user-select:none; -moz-user-select:none; -ms-user-select: none;
}
.onoffswitch-checkbox {
    position: absolute;
    opacity: 0;
    pointer-events: none;
}
.onoffswitch-label {
    display: block; overflow: hidden; cursor: pointer;
    border: 2px solid #999999; border-radius: 20px;
}
.onoffswitch-inner {
    display: block; width: 200%; margin-left: -100%;
    transition: margin 0.3s ease-in 0s;
}
.onoffswitch-inner:before, .onoffswitch-inner:after {
    display: block; float: left; width: 50%; height: 30px; padding: 0; line-height: 30px;
    font-size: 14px; color: white; font-family: Trebuchet, Arial, sans-serif; font-weight: bold;
    box-sizing: border-box;
}
.onoffswitch-inner:before {
    content: "";
    padding-left: 10px;
    background-color: #3445C2; color: #FFFFFF;
}
.onoffswitch-inner:after {
    content: "";
    padding-right: 10px;
    background-color: #EEEEEE; color: #999999;
    text-align: right;
}
.onoffswitch-switch {
    display: block; width: 18px; margin: 6px;
    background: #FFFFFF;
    position: absolute; top: 0; bottom: 0;
    border: 2px solid #999999; border-radius: 20px;
    transition: all 0.3s ease-in 0s; 
}
.onoffswitch-checkbox:checked + .onoffswitch-label .onoffswitch-inner {
    margin-left: 0;
}
.onoffswitch-checkbox:checked + .onoffswitch-label .onoffswitch-switch {
    right: 0px; 
	}
  }
}
}
</style>