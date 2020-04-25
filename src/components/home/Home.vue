<template>
	<div>
		<fs-header></fs-header>
		<fs-content-section></fs-content-section>
	</div>
</template>

<script type="text/javascript">
	import Header from './Header.vue';
	import ContentSection from './ContentSection.vue';

	export default {
		components: {
			'fs-header': Header,
			'fs-content-section': ContentSection
		}
	}
</script>

<style type="text/css" scoped>

</style>
