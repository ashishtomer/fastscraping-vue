<template>
	<div>
		<nav class="navbar" role="navigation" aria-label="main navigation">
				<div class="navbar-brand">
						<a class="navbar-item" href="#o">
								<img src="@/assets/fs-logo-9A1750-with-gradient.png">
						</a>

						<a role="button" class="navbar-burger burger" v-on:click.prevent.stop=displayNavbarMenu aria-label="menu" aria-expanded="false" data-target="navbar">
								<span aria-hidden="true"></span>
								<span aria-hidden="true"></span>
								<span aria-hidden="true"></span>
						</a>
				</div>

				<div id="navbar" class="navbar-menu" v-bind:class="{'is-active' : menuDisplayed}">
						<div class="navbar-end">
								<div class="navbar-item">
										<div class="buttons">
												<a class="button button-color">Contact Us</a>
												<a class="button button-color"	v-on:click.prevent.stop=displayLoginForm>Log in</a>
										</div>
								</div>
						</div>
				</div>
		</nav>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				menuDisplayed: false
			};
		},

		methods: {
			displayNavbarMenu: function() {
				this.menuDisplayed = !this.menuDisplayed;
			}
		}
	}
</script>

<style scoped>
	
</style>