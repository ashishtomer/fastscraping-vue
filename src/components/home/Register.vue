<template>
	<div>
		<div class="register-title"><h1>Register</h1></div>
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

			<div class="field">
				<div class="control">
					<label class="checkbox">
						<input type="checkbox">
						I agree to the <a href="#">terms and conditions</a>
					</label>
				</div>
			</div>

			<div class="field is-grouped">
				<div class="control">
					<input type="submit" class="button register-button" value="Register" v-on:click.prevent="register">
				</div>
				<div class="control">
					<button class="button register-cancel">Cancel</button>
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
			register: function() {
				this.$http.post('localhost')
			}
		}
	}
</script>

<style type="text/css">
	input.register-button {
		background-color: #9A1750;
		color: #fff;
	}

	div.register-title {
		text-align: center;
		font-weight: bold;
		font-size: 30px;
		background-color: #E3E2DF;
		margin-bottom: 1em;
		border-radius: 4px;
		color: #9A1750; 
	}

</style>
