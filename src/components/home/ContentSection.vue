<template>
	<section class="section">

		<div class="columns">
		
			<div class="column  is-two-thirds"><!-- This is the section for infographics --></div>

			<div class="column is-one-third login-signup-form">
				<component v-bind:is="formType"></component>
				<div class="account-message"><span>{{accountQuestion}}? <a href="#" v-on:click.prevent="changeForm">{{linkText}}</a>.</span></div>
			</div>
	
		</div>
	</section>
</template>

<script type="text/javascript">

	import Login from './Login.vue';
	import Register from './Register.vue';

	export default {
		components: {
			'login': Login,
			'register': Register
		},

		data() {
			return {
				formType: 'register',
				accountQuestion: 'Already have an account',
				linkText: 'Login here'
			};
    },

		methods: {
			changeForm: function() {
				if(this.formType == 'register') {
					this.formType = 'login';
					this.accountQuestion = 'Don\'t have an account';
					this.linkText = 'Register here';
				} else {
					this.formType = 'register';
					this.accountQuestion = 'Already have an account';
					this.linkText = 'Login here'
				}
			}
		}

	}
</script>

<style type="text/css" scoped>
	.login-signup-form {
		border: 1px solid #E3E2DF;
		border-radius: 4px;
		padding: 1%;
	}

	.account-message {
		padding: 1em 0em;
		font-size: 0.8em;
	}

	.account-message a {
		color: #EE4C7C;
	}
</style>
