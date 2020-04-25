<template>
	<div class="login-form">
		<div class="login-title"><h1>Login</h1></div>
		<form>
			<div class="field">
				<label class="label">Email</label>
				<div class="control">
					<input class="input" type="email" placeholder="Email input" value="">
				</div>
				<p class="help is-danger" v-bind:class='{"is-invisible":isEmailWarningInvisible}'>This email is invalid</p>
			</div>

			<div class="field">
				<label class="label">Password</label>
				<div class="control">
					<input class="input" type="password" placeholder="Text input">
				</div>
				<p class="help is-danger" v-bind:class='{"is-invisible":isPasswordWarningInvisible}'>This password is invalid</p>
			</div>


			<div class="field is-grouped">
				<div class="control">
					<input type="submit" class="button login-button" value="Login">
				</div>
				<div class="control">
					<button class="button login-cancel">Cancel</button>
				</div>
			</div>
		</form>
	</div>
</template>

<script type="text/javascript">
	export default {
		data() {
			return {
				isEmailWarningInvisible: true,
				isPasswordWarningInvisible: true
			};
		},

		methods: {

		}
	}
</script>

<style type="text/css" scoped>

	input.login-button {
		background-color: #9A1750;
		color: #fff;
	}

	div.login-title {
		text-align: center;
		font-weight: bold;
		font-size: 30px;
		background-color: #E3E2DF;
		margin-bottom: 1em;
		border-radius: 4px;
		color: #9A1750; 
	}

</style>