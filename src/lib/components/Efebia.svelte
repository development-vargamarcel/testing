<script>
	import { onMount } from 'svelte';
	let page = 0;
	let postsData = [];
	let postsContainer;

	let posts = async () => {
		let response = await fetch(
			`https://jsonplaceholder.typicode.com/posts?_page=${page}&_limit=10%60`
		);
		let data = await response.json();
		return data;
	};

	let getNewPostsAndHandle = () => {
		page++;
		posts()
			.then((data) => {
				postsData = [...postsData, ...data];
				console.log(data);
				return data;
			})
			.catch((err) => {
				console.log(err);
			});
	};

	onMount(() => getNewPostsAndHandle());
	let scrolled = () => {
		Math.abs(postsContainer.scrollHeight - postsContainer.clientHeight - postsContainer.scrollTop) <
		1
			? getNewPostsAndHandle()
			: '';
	};
</script>

<div
	bind:this={postsContainer}
	on:scroll={scrolled}
	class="w-full h-screen overflow-y-auto flex flex-col mx-auto px-4 pb-4  "
>
	<div class="h-20 w-1/2 mx-auto shadow-lg sticky top-0 rounded-md p-4 bg-blue-100">
		<h1 class="text-sm md:text-2xl">bellow is the list</h1>
	</div>
	{#each postsData as postData}
		<div class="my-2 mx-auto w-1/2 rounded bg-gray-200 px-2 md:my-4 md:py-2 md:px-4">
			<h3 class="mb-2">
				{postData.id}.
				{postData.title}
			</h3>

			<p class="text-sm">
				{postData.body}
			</p>
		</div>
	{/each}
</div>
