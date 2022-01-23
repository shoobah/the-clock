<script>
	import { onDestroy, onMount } from 'svelte';
	import { format } from 'date-fns-tz';

	const fmt = 'yyyy-MM-dd HH:mm:ss zzzz';
	const timer = setInterval(() => {
		time = new Date();
	}, 1000);
	const getDegrees = (x, xPerR) => (360 / xPerR) * x - 90;

	let time = new Date();

	$: hoursDegrees = getDegrees(time.getHours() * 3600, 24 * 3600);
	$: minuteDegrees = getDegrees(time.getMinutes() * 60, 3600);
	$: secondDegrees = getDegrees(time.getSeconds(), 60);

	onDestroy(() => clearInterval(timer));
</script>

<div>{format(time, fmt)}</div>
<div>{hoursDegrees}</div>
<div>{minuteDegrees}</div>
<div>{secondDegrees}</div>

<div class="face">
	<div class="second_hand" style={`transform: rotate(${secondDegrees}deg) translateX(100px)`}>
		&nbsp;
	</div>
	<div class="minute_hand" style={`transform: rotate(${minuteDegrees}deg) translateX(100px)`}>
		&nbsp;
	</div>
	<div
		class="hour_hand"
		style={`transform: rotate(${hoursDegrees}deg) translateX(50px) translateY(50px)`}
	>
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
		width: 100px;
		height: 4px;
	}
</style>
