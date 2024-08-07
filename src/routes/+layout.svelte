<script>
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
</script>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<strong class="text-xl uppercase">
					<a href="/">Skeleton</a>

				</strong>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<a 
					class="btn btn-sm variant-ghost-surface"
					href="/upload"

				>
				Upload
				</a>
				<a 
					class="btn btn-sm variant-ghost-surface"
					href="/delete"

				>
				Delete
				</a>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>
