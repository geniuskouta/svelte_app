<script>
	import { tick } from 'svelte';
	let recipients = ["aaaa@dsad.com", "djdosa@dsoad.com", "dksoadk@.com", "kofksodpofds@dsad.com"];
	let recipientDisplayList = [];

	let innerWidth = 0;
	let recipientsWidth = 0;

	$: {
		setRecipientDisplayList();
	}

	async function setRecipientDisplayList() {
		for(let i = 0; i < recipients.length; i++) {
			recipientDisplayList.push(recipients[i]);
			recipientDisplayList = recipientDisplayList; // https://svelte.dev/tutorial/updating-arrays-and-objects
			await tick();
			console.log(recipients[i])
			if(recipientsWidth > innerWidth) {
				recipientDisplayList.pop();
				break;
			}	
		}
		await tick();
	}
</script>

<style>
	th, td, table {
		border-collapse: collapse;
		border: 1px solid #333333;
	}

	th, td {
		width: 500px;
		white-space: nowrap;
		text-overflow: ellipsis;
		overflow: hidden;
	}

	.recipients {
		display: inline-block;
	}
</style>

<table>
	<tbody>
		<tr>
			<th>Sender</th>
			<th>Recipients</th>
		</tr>
		<tr>
			<td>Kouta Nakano</td>
			<td>
				<div bind:clientWidth={innerWidth}>
					<span bind:clientWidth={recipientsWidth} class="recipients">
						{#each recipientDisplayList as recipient}
						{recipient},&nbsp
						{/each}
					</span>
				</div>
			</td>
		</tr>
	</tbody>
</table>
