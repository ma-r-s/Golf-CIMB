<script>
	import 'roslib/build/roslib';
	export let ros;
	let color = 'bg-orange-500';
	let direccion = 0;
	let vel = 0;
	let adelante = () => {
		if (vel < 200) {
			vel = Math.round(vel + 20);
		}
		//eslint-disable-next-line
		let twist = new ROSLIB.Message({
			x: direccion,
			y: vel,
			z: 0.0
		});
		//eslint-disable-next-line
		let cmdVel = new ROSLIB.Topic({
			ros: ros,
			name: '/dir',
			messageType: 'geometry_msgs/Vector3'
		});
		cmdVel.publish(twist);
	};
	let atras = () => {
		vel = 0;
		//eslint-disable-next-line
		let twist = new ROSLIB.Message({
			x: direccion,
			y: vel,
			z: 0.0
		});
		//eslint-disable-next-line
		let cmdVel = new ROSLIB.Topic({
			ros: ros,
			name: '/dir',
			messageType: 'geometry_msgs/Vector3'
		});
		cmdVel.publish(twist);
	};
	let izquierda = () => {
		if (direccion < 1) {
			direccion = Math.round((direccion + 0.1) * 10) / 10;
		}

		//eslint-disable-next-line
		let twist = new ROSLIB.Message({
			x: direccion,
			y: vel,
			z: 0.0
		});
		//eslint-disable-next-line
		let cmdVel = new ROSLIB.Topic({
			ros: ros,
			name: '/dir',
			messageType: 'geometry_msgs/Vector3'
		});
		cmdVel.publish(twist);
	};
	let derecha = () => {
		if (direccion > -1) {
			direccion = Math.round((direccion - 0.1) * 10) / 10;
		}
		//eslint-disable-next-line
		let twist = new ROSLIB.Message({
			x: direccion,
			y: vel,
			z: 0.0
		});
		//eslint-disable-next-line
		let cmdVel = new ROSLIB.Topic({
			ros: ros,
			name: '/dir',
			messageType: 'geometry_msgs/Vector3'
		});
		cmdVel.publish(twist);
	};
</script>

<div class="flex items-center gap-10 overflow-hidden">
	<button
		on:click={adelante}
		class=" rounded-full  {color} h-11 w-11 py-2 text-center text-xl font-bold text-white shadow-lg ease-in-out hover:bg-red-600"
	>
		↑
	</button>
	<button
		on:click={atras}
		class=" rounded-full  {color} h-11 w-11 py-2 text-center text-xl font-bold text-white shadow-lg ease-in-out hover:bg-red-600"
	>
		↓
	</button>
	<button
		on:click={izquierda}
		class=" rounded-full  {color} h-11 w-11 py-2 text-center text-xl font-bold text-white shadow-lg ease-in-out hover:bg-red-600"
	>
		←
	</button>
	<button
		on:click={derecha}
		class=" rounded-full  {color} h-11 w-11 py-2 text-center text-xl font-bold text-white shadow-lg ease-in-out hover:bg-red-600"
	>
		→
	</button>
	<div class="font-bold text-white">
		<p>Vel: {vel}</p>
	</div>
	<div class="font-bold text-white">
		<p>Dir: {direccion}</p>
	</div>
</div>
