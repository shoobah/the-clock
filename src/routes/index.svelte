<script>
	import { onDestroy, onMount } from 'svelte';
	import { format } from 'date-fns-tz';

	const fmt = 'yyyy-MM-dd HH:mm:ss zzzz';
	const timer = setInterval(() => {
		time = new Date();
	}, 10);

	let time = new Date();

	$: h = time.getHours();
	$: m = time.getMinutes();
	$: s = time.getSeconds();
	$: ms = time.getMilliseconds();

	$: hoursDegrees = ((h % 12) + m / 60 + s / 3600) * 30 + 90;
	$: minuteDegrees = (m + s / 60 + ms / 60000) * 6 + 90;
	$: secondDegrees = (s + ms / 1000) * 6 + 90;

	onDestroy(() => clearInterval(timer));
</script>

<div>{format(time, fmt)}</div>

<div class="face">
	<div class="second_hand" style={`transform:  rotate(${secondDegrees}deg) translateX(-50%)`}>
		&nbsp;
	</div>
	<div class="minute_hand" style={`transform:  rotate(${minuteDegrees}deg) translateX(-50%)`}>
		&nbsp;
	</div>
	<div class="hour_hand" style={` transform: rotate(${hoursDegrees}deg) translateX(-50%)`}>
		&nbsp;
	</div>
</div>

<style>
	.face {
		position: absolute;
		left: 400px;
		top: 400px;
	}
	.second_hand {
		background-color: pink;
		width: 200px;
		height: 2px;
	}
	.minute_hand {
		background-color: rgb(37, 14, 18);
		width: 200px;
		height: 2px;
	}
	.hour_hand {
		background-color: rgb(20, 94, 33);
		width: 200px;
		height: 4px;
	}
</style>
