# webxr-decal

This is a fork of three.js decal example - modified to work in webxr

https://threejs.org/examples/webgl_decals.html

## Steps

1. enable webxr

Following the threejs doc - https://threejs.org/docs/#manual/en/introduction/How-to-create-VR-content 

- setup renderer for xr
- change render loop from requestAnimationFrame to renderer.setAnimationLoop
- add the vr button

2. scale / move the model

After looking at GLTF model in VR it was huge and in the center of the VR area

- modify scale back from 10 to 1 (original decal demo scaled everything up)
- move the mesh "back" along z

    mesh.position.z = -4;

    scene.add(mesh);
    // mesh.scale.set(10, 10, 10);

3. Add a XR controller

The VR cube example https://threejs.org/examples/webxr_vr_cubes.html does a good job adding a controller and let's copy that in.

4. use controller - interact with the content using "raycasting"

Raycasting in this context means - create a ray starting at your controller in the direction it is facing - and find if/where it intersects with other meshes.

By looking at the mouse raycasting example and the vr cubes raycasting example, I decided to:

- inside the render loop - if `inVR` calculate if the raycast intersections with the head mesh.
- update the mouse raycasting logic to be disabled if `inVR`
- on `selectionStart` (eg, pressing the VR controller button) check if we are intersecting with anything, if so, `shoot`

5. Yay

The splatters might be a bit big still, but I hope this example of using the controller to intersect with objects was fun.