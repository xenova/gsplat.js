# gsplat.js

#### JavaScript Gaussian Splatting library

gsplat.js is an easy-to-use, general-purpose, open-source 3D Gaussian Splatting library, providing functionality similar to [three.js](https://github.com/mrdoob/three.js) but for Gaussian Splatting.

### Demo

A live viewer demo can be found on 🤗 [Hugging Face](https://huggingface.co/spaces/dylanebert/igf). May not work on all devices. Try `Bonsai` for the lowest memory requirements.

### Installation

**Prerequisites**: Ensure your development environment supports ES6 modules.

1. **Set Up a Project:** (If not already set up)

   Install [Node.js](https://nodejs.org/en/download/) and [NPM](https://www.npmjs.com/get-npm), then initialize a new project using a module bundler like [Vite](https://vitejs.dev/):

    ```bash
    npm create vite@latest gsplat -- --template vanilla-ts
    ```

2. **Test Your Environment:**

    ```bash
    cd gsplat
    npm install
    npm run dev
    ```

3. **Install gsplat.js:**

    ```bash
    npm install --save gsplat
    ```

### Usage

#### Creating a Scene

To use **gsplat.js** in your project, follows these steps to create a scene, add a camera, and set up the renderer:

(in `src/main.ts` if you followed the Vite setup)

```js
import * as SPLAT from "gsplat";

const scene = new SPLAT.Scene();
const camera = new SPLAT.Camera();
const renderer = new SPLAT.WebGLRenderer();
const controls = new SPLAT.OrbitControls(camera, renderer.domElement);

async function main() {
    const url = "https://huggingface.co/datasets/dylanebert/3dgs/resolve/main/bicycle/bicycle-7k.splat";

    await SPLAT.Loader.LoadAsync(url, scene, () => {});

    const frame = () => {
        controls.update();
        renderer.render(scene, camera);

        requestAnimationFrame(frame);
    };

    requestAnimationFrame(frame);
}

main();
```

This script sets up a basic scene with Gaussian Splatting data loaded from URL and starts a rendering loop.

### License

This project is released under the MIT license. It is built upon several other open-source projects:

- [three.js](https://github.com/mrdoob/three.js), MIT License (c) 2010-2023 three.js authors
- [antimatter15/splat](https://github.com/antimatter15/splat), MIT License (c) 2023 Kevin Kwok
- [UnityGaussianSplatting](https://github.com/aras-p/UnityGaussianSplatting), MIT License (c) 2023 Aras Pranckevičius

Please note that the license of the original [3D Gaussian Splatting](https://github.com/graphdeco-inria/gaussian-splatting) research project is non-commercial. While this library provides an open-source rendering implementation, users should separately consider where the Splat data comes from.

### Contact

Feel free to open issues, join the [Hugging Face Discord](https://hf.co/join/discord), or email me directly at [dylan@huggingface.co](mailto:dylan@huggingface.co).
