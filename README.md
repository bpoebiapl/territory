# territory
3D rendered proc-gen world test
=======
## Usage
    ./territory [world_name]
If the world name doesn't exist, it will generate a world. If it does, it will load the world. Tested on Ubuntu 18

## Controls
- Change Camera Position: WASD
- Move Camera Up / Down: Space / LShift
- Change View Angle: Scroll Left / Right
- Zoom: Scroll Up / Down

## Panel
- Simulation
	- Control the Simulation Speed
- Population
	- Observe individual bots
		- Follow Bots
		- Check their Task Queue
		- Check the Memory
	- Interrupt Bots
	- Kill Bots
- View
	- Change to perspective projection
	- FPS Counter
	- Change Skybox Color
	- Change Lighting Color

![Example Rendering](https://github.com/weigert/territory/blob/master/territory.png)

## Functionality
### Renderer
- Generation of Voxel Maps based on chunk data
- Proper ignoring of occluded faces for faster VBO (model) construction
- World-Size: 16^3 block-sized chunks, a (10x10x1) chunks ~3.5MB
- Normal Shading
- Shadow Mapping and Transparency
- True 3D Rendering (change angle with arrow keys)
- 2D Camera-Facing Sprites
- Can handle arbitrary LOD for the underlying octree

### World Generator
- Arbitrary Worldsizes
- Chunks saved to file, loaded dynamically when entering regions (change position with WASD), loaded efficiently
- Recursive Octree Data Structure for Chunks, high sparsity of data structure, very compact
- Octree test for majority contents for LOD handling
- Fast macro-world editing using an editBuffer, which sorts changes by their order in file and writes them very quickly
  -> Also tackles the constraint of "chunk-boundaries" and their editing seamlessly for continous objects in world-space
- Simple Perlin Height Generator (for now)

## ToDo:
### Renderer
- Drop-Shadow for sprites
- Sprite animation support
- Sprite Outlines and Block Outlines (-> picking)
- Shader Effects: Fog, Bloom, Blur, Grain, Particles

### Game
- Proper sprite movement constraints

### Event Handler
- Better Handling of Keyboard Inputs (no key-interrupts)
- Simultaneous Action Handling (kinda done, buggy)
- Multi-tick input consequences (i.e. slow moving and animations)

### World Generator
- Geology: Ore Deposits, Stone Types, Solubility / Brittleness, etc / Soil Quality
- Maps: Height, Humidity, Temperature, Volcanism, Drainage, Geology
- Rock: Mountains / Volcanoes / Boulders / Caves / Canyons / Geysers / etc.
- Water: Rivers / Streams / (Hot) Springs / Deltas / Swamps / Islands / Waterfalls
- Biomes: Deserts, Forests, Rainforests, Plains, etc.
- Dynamic Erosion and Flooding
- Dynamic Weather System at chunk resolution(Clouds, Rain, Snow, Hail, Temp, Wind, Lightning, Sunlight)
- Vegetation for soil / water retention, enrichment, climate dependency, cooling
- Dynamic Range of Vegetation, where each plant is a point in some space, then sample near where the state is find nearest plant, place it
