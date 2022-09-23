<script>
	
	let value = []
	$: pagination = value;
	
	const firstPage = 1
	$: currentPage = 1
	$: lastPage = value.length
	
	const getData = async () => {
		await fetch("https://jsonplaceholder.typicode.com/todos")
		.then(response => response.json())
		.then(json => {
			for(let i = 0; i < 200; i++){
				value = [...value, json[i].title]
			}
		})

	}
	
	function next() {
		currentPage++
	}
	
	function previous() {
		currentPage > 1 ? currentPage-- : alert("You can't go back anymore")
	}
	
</script>

{#if value}
	<p>{pagination[currentPage]}</p>
	<p>{pagination[currentPage + 1]}</p>
	<p>{pagination[currentPage + 2]}</p>
	<p>{pagination[currentPage + 3]}</p>
	<p>{pagination[currentPage + 4]}</p>
{/if}

<button on:click={getData}> Click</button>	
<button on:click={previous}>Back</button>
{#if currentPage > 1}
	<button>{currentPage - 1} prev</button>

{/if}
	<button>{currentPage} current</button>
{#if currentPage > 1}
	<button>{currentPage + 1} next </button>
{:else}
	<button>...</button>
{/if}
	<button>{lastPage}</button>
	<button on:click={next}>Next</button>
<style>

</style>