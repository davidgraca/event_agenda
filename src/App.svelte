<script>
	import { getContext } from "svelte";
	import FullCalendar from "svelte-fullcalendar";
	import dayGridPlugin from "@fullcalendar/daygrid";
	import timeGridPlugin from "@fullcalendar/timegrid";
	import interaction from "@fullcalendar/interaction";
	import Modal from "svelte-simple-modal";
	import Content from "./Content.svelte";

	let calendarRef, infoModal, showModal;
	
	function next() {
		let calendarApi = calendarRef.getAPI();
		calendarApi.next();
	}
	let options = {
		initialView: "timeGridWeek",
		plugins: [timeGridPlugin],
		slotMinTime: "09:00:00",
		slotMaxTime: "16:00:00",
		nowIndicator: true,
		initialDate: "2021-10-04",
		validRange: {
			start: "2021-10-04",
			end: "2021-10-15",
		},
		events: function (info, successCallback, failureCallback) {
			console.log(info);
			fetch("./data-sample.json")
				.then((response) => response.json())
				.then((data) => {
					console.log(data);
					successCallback(data);
				})
				.catch((err) => failureCallback(err));
		},
		eventClick: function (info) {

			infoModal = {
				title: info.event.title,
				start: info.event.start,
				end: info.event.end,
				other: info.event.extendedProps,
			};
			showModal=true;
		},
	};
</script>

<main class="container">
	<h1>AXA Software Engineering Summit 2021!</h1>
	<FullCalendar bind:this={calendarRef} {options} />
	<Modal >
		<Content bind:info={infoModal} {showModal}/>
	</Modal>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
