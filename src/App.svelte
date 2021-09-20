<script>
	import FullCalendar from "svelte-fullcalendar";
	import dayGridPlugin from "@fullcalendar/daygrid";
	import timeGridPlugin from "@fullcalendar/timegrid";
	import interaction from "@fullcalendar/interaction";
	import Modal from "svelte-simple-modal";
	import Content from "./Content.svelte";

	let calendarRef, infoModal, showModal;
	let targetAudienceFilter = [],
		tagFilter = [],
		selectedTargetAudienceFilter = [],
		selectedTagFilter = [];
	let calendarApi = function () {
		return calendarRef.getAPI();
	};

	function next() {
		calendarApi()().next();
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
			showModal = true;
		},
		
	};

	// Extract filters
	fetch("./data-sample.json")
		.then((response) => response.json())
		.then((data) => {
			console.log(data);
			let uniqueDictTags = {};
			data.forEach((session) =>
				session.tags.forEach((tag) => (uniqueDictTags[tag] = 1))
			);
			tagFilter = Object.keys(uniqueDictTags);

			let uniqueDictTargetAudience = {};
			data.forEach((session) =>
				session.target_audience.forEach(
					(ta) => (uniqueDictTargetAudience[ta] = 1)
				)
			);
			targetAudienceFilter = Object.keys(uniqueDictTargetAudience);
		})
		.catch((err) => console.log(err));
	$: {
		console.log(selectedTagFilter);
		console.log(selectedTargetAudienceFilter);
	}
	function handleChange() {
		calendarApi().batchRendering(function () {
			let events = calendarApi().getEvents();
			/* erase visibility */
			for (let i = 0; i < events.length; i++) {
				let event = events[i];
				event.setProp("display", "auto");
			}
			/* hide the ones not matching */
			for (let i = 0; i < events.length; i++) {
				let event = events[i];
				if (
					selectedTagFilter.length != 0 &&
					selectedTagFilter.find((el) =>
						event.extendedProps.tags.includes(el)
					) == undefined
				) {
					event.setProp("display", "none");
				}
				if (
					selectedTargetAudienceFilter.length != 0 &&
					selectedTargetAudienceFilter.find((el) =>
						event.extendedProps.target_audience.includes(el)
					) == undefined
				) {
					event.setProp("display", "none");
				}
			}
		});
	}
</script>

<main class="container-fluid">
	<div class="row">
		<div class="col">
			<h1>SE Summit 2021: Agenda</h1>
		</div>
	</div>
	<div class="row">
		<div class="col-sm-auto">
			<form>
				<b>Tags</b>
				{#each tagFilter as filter}
					<div class="form-check">
						<input
							class="form-check-input"
							type="checkbox"
							id={filter}
							value={filter}
							bind:group={selectedTagFilter}
							on:change={handleChange}
						/>
						<label class="form-check-label" for={filter}
							>{filter}</label
						>
					</div>
				{/each}
				<b>Target Audience</b>
				{#each targetAudienceFilter as filter}
					<div class="form-check">
						<input
							class="form-check-input"
							type="checkbox"
							id={filter}
							value={filter}
							bind:group={selectedTargetAudienceFilter}
							on:change={handleChange}
						/>
						<label class="form-check-label" for={filter}
							>{filter}</label
						>
					</div>
				{/each}
			</form>
		</div>
		<div class="col">
			<FullCalendar bind:this={calendarRef} {options} />
			<Modal>
				<Content bind:info={infoModal} {showModal} />
			</Modal>
		</div>
	</div>
</main>

<style>

</style>
