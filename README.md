# Ray Optics Simulation - Student version

Ray Optics Simulation is a web app for creating and simulating 2D geometric optical scenes. Ray Optics Simulation - Student version is a fork of the project made with the intention of making it easier for students to use and to allow embedding simulations into learning materials. Please view the NOTICE and RayOpticsChanges.txt files for a list of changes.

# [Link to the original project](https://github.com/ricktu288/ray-optics)

# Demo: [optikasimulatsioonid.netlify.app](https://optikasimulatsioonid.netlify.app/)

## Project structure

- `src` contains the source code for the project.
- `data` contains the data for gallery, modules, and the list of contributors.
- `locales` contains the translations for the project in i18next format, managed by Weblate.
- `scripts` contains the scripts for custom build steps.
- `test` contains the automatic tests for the project.
- `dist` (generated at build time) contains the built files for the project (the entire content for the [https://phydemo.app/ray-optics](https://phydemo.app/ray-optics) website).
- `dist-node` (generated at build time) contains the built files for the node module version of the simulator, which is required for the image generation, and can also be used in your own project.

See the README.md in each directory for more information.

## Development

For development of the web app, you can just use `npm run start`, and the web app will be automatically reloaded when some code for the simulator is modified. However, to rebuild some other part of this project, you need to run the following commands:
```bash
# build home pages, about pages, gallery, and modules pages (not including scenes and image generation).
npm run build-webpages

# build the scenes for the gallery and modules pages.
npm run build-scenes

# build the node module version of the simulator, which is required for the image generation.
npm run build-node

# generate images for the gallery, which may take a long time.
npm run build-images

# build the web app version of simulator (unlike npm run start, this command builds the simulator in production mode)
npm run build-simulator

# build documentation
npm run build-docs
```
Note that `npm run build` is equivalent to running all the above commands.

## Testing

To run the automatic tests,
```bash
npm run test
```
The tests are run automatically when you commit your changes.

The above command will run the following tests:
```bash
npm run test:sceneObjs
npm run test:scenes
```
the first one tests the user creation, dragging, and changing properties for each scene object in the source code.
the second one runs the scene JSONs in `test/scenes/` with the node module version of the simulator, and compares the output of `CropBox`/`Detector` with the corresponding PNG/CSV files.

If you modify the appearance of some objects or rays, the images in `test/scenes/` may need to be updated. Also if you add new scene tests, the corresponding PNG and CSV files nees to be initialized. In these cases, run the following command to regenerate all the PNG/CSV files after you make sure that all the failing tests are due to the changes you made:
```bash
env WRITE_OUTPUT=true npm run test:scenes
```
Please do not run this command if you are not sure that all the failing tests are due to the changes you made, since after running it, all scene tests will pass vacuously.

Currently there is no automatic end-to-end test for the web app. So please manually check that the UI works as expected if you make any changes.

## Use as a Node Module

The simulator can be used as a node module in your own project. The node module version of the simulator is built with the following command:
```bash
npm run build-node
```
After that, you can use the simulator in your own project by importing the module:
```javascript
const { Scene, Simulator, sceneObjs, geometry } = require('path/to/ray-optics/dist-node/main.js');
```

See the [documentation](https://phydemo.app/ray-optics/docs/index.html) for more information about the API. For a usage example, see the [image generation script](https://github.com/ricktu288/ray-optics/blob/master/scripts/buildImages.mjs).


## License

```
Copyright 2016–2025 The Ray Optics Simulation authors and contributors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
