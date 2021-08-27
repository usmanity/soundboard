<script>
	// array of A - Z
	var alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');
	var filePath = null;

	function something(letter) {
		console.log('ok clicked', letter);
	}

	function createAudioElement(letter, e) {}

	function uploadFile(file) {
		var fileObj = file[0];
		filePath = URL.createObjectURL(fileObj);
	}

	function keyDownHandler(event) {
		var key = event.keyCode;
		let letter = String.fromCharCode(key);
		if (alphabet.indexOf(letter) > -1) {
			something(letter);
		}
	}

  function getLetterAudio(letter) {

  }
</script>

<svelte:window on:keydown={keyDownHandler} />
<div>
	<!-- loops over `alphabet` array with a for loop -->
	<div>
		<h2>Alphabet</h2>
		<div class="alphabet">
			{#each alphabet as letter, key}
				<li on:click={() => something(letter)}>
					{letter}
					<div>
						<input type="file" on:change={(e) => uploadFile(e.target.files, letter)} />
					</div>
					<div class="player">
						<audio src={() => getLetterAudio(letter)} controls="false" />
					</div>
				</li>
			{/each}
		</div>
	</div>
</div>

<style>
	.alphabet {
		display: flex;
		flex-wrap: wrap;
	}
	.alphabet li {
		width: 200px;
		list-style: none;
	}
	.alphabet li:hover {
		background-color: #f0f0f0;
		cursor: pointer;
	}
	.player {
		margin-top: 30px;
    width: 30px;
	}
</style>
