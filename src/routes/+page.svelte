<script lang="ts">
	import dayjs from 'dayjs';
	import utc from 'dayjs/plugin/utc';
	import timezone from 'dayjs/plugin/timezone';
	import { onMount } from 'svelte';

	dayjs.extend(utc);
	dayjs.extend(timezone);

	let guess_tz = dayjs.tz.guess();
	dayjs.tz.setDefault(guess_tz);
	let dayjsnow = dayjs();
	let refreshIntervalTimeMs = 1000;

	$: time = dayjsnow.format('d MMMM YYYY HH:mm:ss');

	onMount(() => {
		setInterval(() => {
			dayjsnow = dayjs();
		}, refreshIntervalTimeMs);
	});
</script>

<div class="px-4 my-4 w-full">
	<div class="w-1/2">
		<h1
			class="border-2 border-slate-400 mb-8 font-bold text-2xl px-4 py-2 w-fit rounded-md shadow-md"
		>
			{guess_tz}: {time}
		</h1>
		<h1 class="font-bold text-2xl px-4 py-2 w-fit rounded-full">
			America/Vancouver: {dayjsnow.tz('America/Vancouver').format('d MMMM YYYY HH:mm:ss')}
		</h1>
		<h1 class="font-bold text-2xl px-4 py-2 w-fit rounded-full">
			Asia/Kolkata: {dayjsnow.tz('Asia/Kolkata').format('d MMMM YYYY HH:mm:ss')}
		</h1>
		<h1 class="font-bold text-2xl px-4 py-2 w-fit rounded-full">
			Australia/Sydney: {dayjsnow.tz('Australia/Sydney').format('d MMMM YYYY HH:mm:ss')}
		</h1>
		<h1 class="font-bold text-2xl px-4 py-2 w-fit rounded-full">
			Europe/Dublin: {dayjsnow.tz('Europe/Dublin').format('d MMMM YYYY HH:mm:ss')}
		</h1>
	</div>
</div>
