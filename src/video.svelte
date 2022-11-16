<script>

	let audio = new Audio("/music.m4a");
	
	let time = 0;
	let duration;
	let paused = true;

	let showControls = true;
	let showControlsTimeout;

	let lastMouseDown;

	let audioPlay = false;

	function handleMove(e) {
		clearTimeout(showControlsTimeout);
		showControlsTimeout = setTimeout(() => showControls = false, 2500);
		showControls = true;

		if (!duration) return;
		if (e.type !== 'touchmove' && !(e.buttons & 1)) return; 

		const clientX = e.type === 'touchmove' ? e.touches[0].clientX : e.clientX;
		const { left, right } = this.getBoundingClientRect();
		time = duration * (clientX - left) / (right - left);
	}
	function handleMousedown(e) {
		lastMouseDown = new Date();
	}

	function handleMouseup(e) {
		if (new Date() - lastMouseDown < 300) {
			if (paused) e.target.play();
			else e.target.pause();
		}
	}

	function format(seconds) {
		if (isNaN(seconds)) return '...';

		const minutes = Math.floor(seconds / 60);
		seconds = Math.floor(seconds % 60);
		if (seconds < 10) seconds = '0' + seconds;

		return `${minutes}:${seconds}`;
	}

	function audioToggle(){
		if(audioPlay === false){
			audio.play();
			audioPlay = true;
		} else {
			audio.pause();
			audio.currentTime = 0;
			audioPlay = false;
		}
	}

</script>

<h1>Landscape Video</h1>

<!-- <div> -->
	<!-- <video
		poster="/Pines.png"
		src="/Pines.mov"
		on:mousemove={handleMove}
		on:touchmove|preventDefault={handleMove}
		on:mousedown={handleMousedown}
		on:mouseup={handleMouseup}
		bind:currentTime={time}
		bind:duration
		bind:paused>
		<track kind="captions">
	</video> -->

	<!-- <div class="controls" style="opacity: {duration && showControls ? 1 : 0}">
		<progress value="{(time / duration) || 0}"/>

		<div class="info">
			<span class="time">{format(time)}</span>
			<span class="time">{format(duration)}</span>
		</div>
	</div>
</div> -->

<h1>Music Sample</h1>
	
<button on:click={audioToggle}>{audioPlay ? `Stop Audio` : `Play Audio`}</button>

<style>
	div {
		position: relative;
	}

	.controls {
		position: absolute;
		top: 0;
		width: 100%;
		transition: opacity 1s;
	}

	.info {
		display: flex;
		width: 100%;
		justify-content: space-between;
	}

	span {
		padding: 0.2em 0.5em;
		color: white;
		text-shadow: 0 0 8px black;
		font-size: 1.4em;
		opacity: 0.7;
	}

	.time {
		width: 3em;
	}

	.time:last-child { text-align: right }

	progress {
		display: block;
		width: 100%;
		height: 10px;
		-webkit-appearance: none;
		appearance: none;
	}

	progress::-webkit-progress-bar {
		background-color: rgba(0,0,0,0.2);
	}

	progress::-webkit-progress-value {
		background-color: rgba(255,255,255,0.6);
	}

	video {
		width: 100%;
	}
</style>

