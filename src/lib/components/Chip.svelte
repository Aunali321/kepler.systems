<script lang="ts">
	export let name: string | number;
</script>

<div class="chip" itemprop="disambiguatingDescription">
	{name}
</div>

<style lang="scss">
	.chip {
		background: rgba(0, 255, 213, 0.1);
		border: 1px solid var(--primary-dark);
		color: var(--primary);
		border-radius: 4px;
		padding: 0.5rem 1rem;
		font-size: 0.875rem;
		transition: all 0.3s ease;
		margin: 0 0.5rem 0.5rem 0;

		&:hover {
			background: rgba(0, 255, 213, 0.15);
			transform: translateY(-1px);
		}
	}
</style>
