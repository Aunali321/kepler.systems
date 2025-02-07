<script lang="ts">
	export let name: string | number;
</script>

<div class="chip" itemprop="disambiguatingDescription">
	{name}
</div>

<style lang="scss">
	.chip {
		font-family: var(--font-two);
		letter-spacing: -0.06em;
		font-size: 0.875rem;
		background-color: var(--neutral-one);
		color: var(--white);
		border-radius: 2px;
		padding: 0.25rem 0.5rem;
		display: flex;
		gap: 0.1rem;
		align-items: center;
		max-height: 28px;
	}
</style>