<script>
	import sms from 'cordova-sms-plugin'

	export let number = null, message = null

	function requestSmsPermission() {
		let success = function (hasPermission) {
			if (!hasPermission) {
				sms.requestPermission(function() {
					console.log('[OK] Permission accepted')
				}, function(error) {
					console.info('[WARN] Permission not accepted')
				})
			}
		};
		let error = function (e) { alert('Something went wrong:' + e); };
		sms.hasPermission(success, error);
	}

	function sendSms() {
		let success = function (hasPermission) {
			if (hasPermission) {
				console.log("number=" + number + ", message= " + message);

				let options = {
					replaceLineBreaks: false,
					android: {
						intent: ''
						// send SMS without opening any other app, require : android.permission.SEND_SMS and android.permission.READ_PHONE_STATE
					}
				};

				let success = function () { console.log('Message sent successfully'); };
				let error = function (e) { console.log('Message Failed:' + e); };
				sms.send(number, message, options, success, error);
			}
			else {
				console.info('[WARN] Permission not accepted')
			}
		};
		let error = function (e) { console.log('Something went wrong:' + e); };
		sms.hasPermission(success, error);
	}
</script>

<main>
	<p>Enter phone number</p>
	<input bind:value={number} type="tel">

	<p>Enter message</p>
	<input bind:value="{message}">

	<pre>Number: {number} Message: {message}</pre>

	<button on:click={requestSmsPermission}>Request SMS Permission</button>
	<button on:click={sendSms}>Send SMS</button>

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>