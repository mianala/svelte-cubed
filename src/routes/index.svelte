<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';

	const modelURL = '/scene.gltf';
	let model = null;

	function loadGLTF() {
		const loader = new GLTFLoader();
		return loader.loadAsync(modelURL);
	}

	onMount(() => {
		loadGLTF().then((_model) => (model = _model));
	});
</script>

​<SC.Canvas
	antialias
	background={new THREE.Color('papayawhip')}
	shadows
	fog={new THREE.FogExp2('papayawhip', 0.07)}
>
	<SC.Group position={[0, -6, 0]}>
		<SC.Mesh
			geometry={new THREE.PlaneGeometry(50, 50)}
			material={new THREE.MeshStandardMaterial({ color: 'burlywood' })}
			rotation={[-Math.PI / 2, 0, 0]}
			scale={[1, 1, 1]}
			receiveShadow
		/>

		<SC.Primitive
			object={new THREE.GridHelper(50, 50, 0x444444, 0x555555)}
			position={[0, 0.001, 0]}
		/>
	</SC.Group>
	<SC.Primitive
		object={model.scene}
		scale={[0.5, 0.5, 0.5]}
		position={[2.7, -10, -2]}
		rotation={[0, 0, 0]}
	/>
	<SC.PerspectiveCamera position={[0, -2, 13]} />
	<SC.OrbitControls enableZoom={true} />
	<SC.AmbientLight intensity={1} />
	<SC.DirectionalLight shadow={{ mapSize: [2048, 2048] }} intensity={0.6} position={[-2, 3, 2]} />
</SC.Canvas>
