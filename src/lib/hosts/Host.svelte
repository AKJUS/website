<script lang="ts">
	import HostSocialLink from './HostSocialLink.svelte';
	interface Props {
		guest?: boolean;
		host: {
		name: string;
		github?: string | null;
		twitter?: string | null;
		slug?: string;
	};
	}

	let { guest = false, host }: Props = $props();
</script>

<div class="person">
	<figure>
		<!--Kind of an interesting exemption to this: https://twitter.com/wesbos/status/1831327448266326385 -->
		<img src={`https://github.com/${host.github}.png`} alt={host.name} role="presentation" />
		<figcaption>
			<p>
				{#if guest}
					<a href={`/guest/${host.slug}`}>{host.name}</a>
				{:else}
					{host.name}
				{/if}
				<span class="host-guest-tag fst-900-i grit">{guest ? 'Guest' : 'Host'}</span>
			</p>
			<div class="featuring_socials">
				<HostSocialLink {host} />
			</div>
		</figcaption>
	</figure>
</div>

<style lang="postcss">
	.person {
		border: 1px solid var(--line);
		border-radius: 50px;
		position: relative;
		border-left: 0;
		padding-right: 0.5rem;
	}
	figure {
		display: grid;
		grid-template-columns: 70px 1fr;
		margin: 0;
	}

	figure img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 50%;
	}

	figcaption {
		padding: 10px;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	figcaption p {
		margin: 0;
		white-space: nowrap;
		display: flex;
		align-items: center;
		gap: 0.5rem;
	}

	.host-guest-tag {
		background: var(--yellow);
		color: var(--black);
		padding: 0 4px;
		transform: rotate(-3deg);
		font-size: var(--font-size-xs);
	}
</style>
