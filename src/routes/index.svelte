<script>
	var alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');
  var fileStorage = {};

	function playSound(letter) {
		console.log('tapped', letter);
    var player = document.getElementsByClassName(`${letter}-player`)[0];
    player.play();
	}

	function createAudioElement(letter, filePath) {
    var audio = document.getElementsByClassName(`${letter}-player`)[0];
    audio.setAttribute('src', filePath);
    return audio;
  }

	function uploadFile(file, letter) {
		var fileObj = file[0];
    var filePath = URL.createObjectURL(fileObj);
    fileStorage[letter] = filePath;
    console.log(fileStorage);
    createAudioElement(letter, filePath);
	}

	function keyDownHandler(event) {
		var key = event.keyCode;
		let letter = String.fromCharCode(key);
		if (alphabet.indexOf(letter) > -1) {
			playSound(letter);
		}
	}

  function getFirstLetter() {
    for (var i = 0; i < alphabet.length; i++) {
      if (!fileStorage[alphabet[i]]) {
        return alphabet[i];
      }
    }
  }

  function getLetterAudio(letter) {
    return fileStorage[letter] ? fileStorage[letter] : '';
  }
</script>

<svelte:window on:keydown={keyDownHandler} />
<div>
	<!-- loops over `alphabet` array with a for loop -->
	<div>
		<h2>Local sound player</h2>
		<div class="alphabet">
			{#each alphabet as letter, key}
				<!-- <li on:click={() => playSound(letter)}> -->
        <li>
					{letter}
					<div>
						<input type="file" on:change={(e) => uploadFile(e.target.files, letter)} />
					</div>
					<div class="player">
						<audio class={letter + '-player'}/>
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
  * {
    font-family: 'Inter', sans-serif;
  }
</style>
