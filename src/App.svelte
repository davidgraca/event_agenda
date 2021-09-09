<script>
	import { getContext } from "svelte";
	import FullCalendar from "svelte-fullcalendar";
	import dayGridPlugin from "@fullcalendar/daygrid";
	import timeGridPlugin from "@fullcalendar/timegrid";
	import interaction from "@fullcalendar/interaction";
	import Modal from "svelte-simple-modal";
	import Content from "./Content.svelte";

var saveAs=saveAs||function(e){"use strict";if(typeof e==="undefined"||typeof navigator!=="undefined"&&/MSIE [1-9]\./.test(navigator.userAgent)){return}var t=e.document,n=function(){return e.URL||e.webkitURL||e},r=t.createElementNS("http://www.w3.org/1999/xhtml","a"),o="download"in r,a=function(e){var t=new MouseEvent("click");e.dispatchEvent(t)},i=/constructor/i.test(e.HTMLElement)||e.safari,f=/CriOS\/[\d]+/.test(navigator.userAgent),u=function(t){(e.setImmediate||e.setTimeout)(function(){throw t},0)},s="application/octet-stream",d=1e3*40,c=function(e){var t=function(){if(typeof e==="string"){n().revokeObjectURL(e)}else{e.remove()}};setTimeout(t,d)},l=function(e,t,n){t=[].concat(t);var r=t.length;while(r--){var o=e["on"+t[r]];if(typeof o==="function"){try{o.call(e,n||e)}catch(a){u(a)}}}},p=function(e){if(/^\s*(?:text\/\S*|application\/xml|\S*\/\S*\+xml)\s*;.*charset\s*=\s*utf-8/i.test(e.type)){return new Blob([String.fromCharCode(65279),e],{type:e.type})}return e},v=function(t,u,d){if(!d){t=p(t)}var v=this,w=t.type,m=w===s,y,h=function(){l(v,"writestart progress write writeend".split(" "))},S=function(){if((f||m&&i)&&e.FileReader){var r=new FileReader;r.onloadend=function(){var t=f?r.result:r.result.replace(/^data:[^;]*;/,"data:attachment/file;");var n=e.open(t,"_blank");if(!n)e.location.href=t;t=undefined;v.readyState=v.DONE;h()};r.readAsDataURL(t);v.readyState=v.INIT;return}if(!y){y=n().createObjectURL(t)}if(m){e.location.href=y}else{var o=e.open(y,"_blank");if(!o){e.location.href=y}}v.readyState=v.DONE;h();c(y)};v.readyState=v.INIT;if(o){y=n().createObjectURL(t);setTimeout(function(){r.href=y;r.download=u;a(r);h();c(y);v.readyState=v.DONE});return}S()},w=v.prototype,m=function(e,t,n){return new v(e,t||e.name||"download",n)};if(typeof navigator!=="undefined"&&navigator.msSaveOrOpenBlob){return function(e,t,n){t=t||e.name||"download";if(!n){e=p(e)}return navigator.msSaveOrOpenBlob(e,t)}}w.abort=function(){};w.readyState=w.INIT=0;w.WRITING=1;w.DONE=2;w.error=w.onwritestart=w.onprogress=w.onwrite=w.onabort=w.onerror=w.onwriteend=null;return m}(typeof self!=="undefined"&&self||typeof window!=="undefined"&&window||this.content);if(typeof module!=="undefined"&&module.exports){module.exports.saveAs=saveAs}else if(typeof define!=="undefined"&&define!==null&&define.amd!==null){define("FileSaver.js",function(){return saveAs})}

    var ics=function(e,t){"use strict";{if(!(navigator.userAgent.indexOf("MSIE")>-1&&-1==navigator.userAgent.indexOf("MSIE 10"))){void 0===e&&(e="default"),void 0===t&&(t="Calendar");var r=-1!==navigator.appVersion.indexOf("Win")?"\r\n":"\n",n=[],i=["BEGIN:VCALENDAR","PRODID:"+t,"VERSION:2.0"].join(r),o=r+"END:VCALENDAR",a=["SU","MO","TU","WE","TH","FR","SA"];return{events:function(){return n},calendar:function(){return i+r+n.join(r)+o},addEvent:function(t,i,o,l,u,s){if(void 0===t||void 0===i||void 0===o||void 0===l||void 0===u)return!1;if(s&&!s.rrule){if("YEARLY"!==s.freq&&"MONTHLY"!==s.freq&&"WEEKLY"!==s.freq&&"DAILY"!==s.freq)throw"Recurrence rrule frequency must be provided and be one of the following: 'YEARLY', 'MONTHLY', 'WEEKLY', or 'DAILY'";if(s.until&&isNaN(Date.parse(s.until)))throw"Recurrence rrule 'until' must be a valid date string";if(s.interval&&isNaN(parseInt(s.interval)))throw"Recurrence rrule 'interval' must be an integer";if(s.count&&isNaN(parseInt(s.count)))throw"Recurrence rrule 'count' must be an integer";if(void 0!==s.byday){if("[object Array]"!==Object.prototype.toString.call(s.byday))throw"Recurrence rrule 'byday' must be an array";if(s.byday.length>7)throw"Recurrence rrule 'byday' array must not be longer than the 7 days in a week";s.byday=s.byday.filter(function(e,t){return s.byday.indexOf(e)==t});for(var c in s.byday)if(a.indexOf(s.byday[c])<0)throw"Recurrence rrule 'byday' values must include only the following: 'SU', 'MO', 'TU', 'WE', 'TH', 'FR', 'SA'"}}var g=new Date(l),d=new Date(u),f=new Date,S=("0000"+g.getFullYear().toString()).slice(-4),E=("00"+(g.getMonth()+1).toString()).slice(-2),v=("00"+g.getDate().toString()).slice(-2),y=("00"+g.getHours().toString()).slice(-2),A=("00"+g.getMinutes().toString()).slice(-2),T=("00"+g.getSeconds().toString()).slice(-2),b=("0000"+d.getFullYear().toString()).slice(-4),D=("00"+(d.getMonth()+1).toString()).slice(-2),N=("00"+d.getDate().toString()).slice(-2),h=("00"+d.getHours().toString()).slice(-2),I=("00"+d.getMinutes().toString()).slice(-2),R=("00"+d.getMinutes().toString()).slice(-2),M=("0000"+f.getFullYear().toString()).slice(-4),w=("00"+(f.getMonth()+1).toString()).slice(-2),L=("00"+f.getDate().toString()).slice(-2),O=("00"+f.getHours().toString()).slice(-2),p=("00"+f.getMinutes().toString()).slice(-2),Y=("00"+f.getMinutes().toString()).slice(-2),U="",V="";y+A+T+h+I+R!=0&&(U="T"+y+A+T,V="T"+h+I+R);var B,C=S+E+v+U,j=b+D+N+V,m=M+w+L+("T"+O+p+Y);if(s)if(s.rrule)B=s.rrule;else{if(B="rrule:FREQ="+s.freq,s.until){var x=new Date(Date.parse(s.until)).toISOString();B+=";UNTIL="+x.substring(0,x.length-13).replace(/[-]/g,"")+"000000Z"}s.interval&&(B+=";INTERVAL="+s.interval),s.count&&(B+=";COUNT="+s.count),s.byday&&s.byday.length>0&&(B+=";BYDAY="+s.byday.join(","))}(new Date).toISOString();var H=["BEGIN:VEVENT","UID:"+n.length+"@"+e,"CLASS:PUBLIC","DESCRIPTION:"+i,"DTSTAMP;VALUE=DATE-TIME:"+m,"DTSTART;VALUE=DATE-TIME:"+C,"DTEND;VALUE=DATE-TIME:"+j,"LOCATION:"+o,"SUMMARY;LANGUAGE=en-us:"+t,"TRANSP:TRANSPARENT","END:VEVENT"];return B&&H.splice(4,0,B),H=H.join(r),n.push(H),H},download:function(e,t){if(n.length<1)return!1;t=void 0!==t?t:".ics",e=void 0!==e?e:"calendar";var a,l=i+r+n.join(r)+o;if(-1===navigator.userAgent.indexOf("MSIE 10"))a=new Blob([l]);else{var u=new BlobBuilder;u.append(l),a=u.getBlob("text/x-vCalendar;charset="+document.characterSet)}return saveAs(a,e+t),l},build:function(){return!(n.length<1)&&i+r+n.join(r)+o}}}console.log("Unsupported Browser")}};

	let cal = ics();
	cal.addEvent('Demo Event', 'This is an all day event', 'Nome, AK', '8/7/2013', '8/7/2013');
	cal.addEvent('Demo Event', 'This is thirty minute event', 'Nome, AK', '8/7/2013 5:30 pm', '8/7/2013 6:00 pm');
	
function download(){
	cal.download("Multiple");
}

	let calendarRef, infoModal, showModal;
	let targetAudienceFilter = [],
		tagFilter = [],
		selectedTargetAudienceFilter = [],
		selectedTagFilter = [];
	let calendarApi = function(){ return calendarRef.getAPI();}

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
		headerToolbar: {
      left: 'prev,next today filter unfilter',
      center: 'title',
      right: 'resourceTimelineDay,resourceTimeGridDay'
    },
    customButtons: {
      filter: {
        text: 'Apply filters',
        click: function() {
			calendarApi().batchRendering(function() {
            let events = calendarApi().getEvents()
            for (let i = 0; i < events.length; i++) {
              let event = events[i]
              if (selectedTagFilter.length != 0 && selectedTagFilter.find( el => event.extendedProps.tags.includes(el)) == undefined) {
                event.setProp('display', 'none')
              }
			  if (selectedTargetAudienceFilter.length != 0 && selectedTargetAudienceFilter.find(el => event.extendedProps.target_audience.includes(el))== undefined) {
                event.setProp('display', 'none')
              }
            }
          })
        }
      },
      unfilter: {
        text: 'Remove filters',
        click: function() {
			calendarApi().batchRendering(function() {
            let events = calendarApi().getEvents();
            for (let i = 0; i < events.length; i++) {
              let event = events[i];
			  event.setProp('display', 'auto');
            }
			selectedTagFilter =[];
			selectedTargetAudienceFilter = [];
          })
        }
      } 
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
		$:{
			console.log(selectedTagFilter);
			console.log(selectedTargetAudienceFilter);
			
		}

</script>

<main class="container">
	<h1>AXA Software Engineering Summit 2021!</h1>
	
	<span>Tags</span><br>
	{#each tagFilter as filter}
	<span>{filter}</span>
		<input type="checkbox" id={filter} value={filter} bind:group={selectedTagFilter} /> 
	{/each}
	<br><span>Target Audience</span><br>
	{#each targetAudienceFilter as filter}
	<span>{filter}</span>
		<input type="checkbox" id={filter} value={filter} bind:group={selectedTargetAudienceFilter}/>
	{/each}
	<FullCalendar bind:this={calendarRef} {options} />
	<Modal>
		<Content bind:info={infoModal} {showModal} />
	</Modal>
	<a href="#" on:click="{download}">Download as Outlook calendar</a>
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
