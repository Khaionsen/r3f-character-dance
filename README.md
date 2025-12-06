https://github.com/Khaionsen/r3f-character-dance/releases

# r3f Character Dance — Creative Motion Effects for React Three Fiber

![Hero](https://picsum.photos/1200/420?grayscale&random=1)

A character dance effect to improve my R3F skills. This project mixes real-time 3D motion with playful choreography to explore animation techniques in React Three Fiber.

[![Releases](https://img.shields.io/github/v/release/Khaionsen/r3f-character-dance?style=for-the-badge&color=brightgreen&label=Releases)](https://github.com/Khaionsen/r3f-character-dance/releases)
[![License](https://img.shields.io/github/license/Khaionsen/r3f-character-dance?style=for-the-badge&color=blue)](https://github.com/Khaionsen/r3f-character-dance/blob/main/LICENSE)
[![Contributors](https://img.shields.io/github/contributors/Khaionsen/r3f-character-dance?style=for-the-badge&color=orange)](https://github.com/Khaionsen/r3f-character-dance/graphs/contributors)

This repository hosts a compact, expressive character dance effect built with React Three Fiber. It demonstrates how to coordinate character motion with a dynamic environment, using a lightweight animation system that is friendly to experiments and rapid iteration.

Table of contents
- About this project
- Core ideas and design choices
- How it works under the hood
- Getting started
- Installation and setup
- Running locally
- API and components
- Customization and theming
- Animations and motion details
- Scene composition
- Assets and releases
- Development workflow
- Testing and quality
- Accessibility and usability
- Performance considerations
- Debugging tips
- Examples and patterns
- Contributing
- Roadmap
- License and credits

About this project
r3f Character Dance is a small, focused project meant to be approachable but also deep enough for serious experimentation. It presents a character model performing a sequence of choreographed moves. The dance is driven by a simple motion graph, a set of easing curves, and a handful of pose targets. The goal is to provide a clear playground where artists and developers can push the limits of real-time animation in the browser.

The project is built with modern web technologies. React provides the UI layer, while React Three Fiber renders 3D content using Three.js underneath. WebGL and WebGL2 capabilities enable smooth rendering of complex shapes, lighting, and materials. TypeScript enforces type safety for components and data structures, helping you reason about the motion graph and scene graph with confidence. The result is a cohesive tool that blends code, math, and art in a single, accessible package.

Core ideas and design choices
- Simplicity first: The core dancer is a self-contained component that can be dropped into any scene. It exposes a small, predictable API and sensible defaults.
- Modularity: The dancer relies on a motion graph and a set of pose targets. You can swap in new poses or new motion rules without rewriting the entire system.
- Expandability: The library is designed to be extended. You can add new limbs, new easing curves, or alternate control schemes without breaking existing usage.
- Reproducibility: The motion graph and pose cues are deterministic given the same seed and inputs. This makes it easy to reproduce scenarios for testing and sharing.
- Accessibility: Textures, lighting, and controls are chosen with clarity in mind. The dance remains legible even on devices with modest GPU power.

How it works under the hood
- Scene graph: The dancer attaches to a Three.js scene through React Three Fiber, integrating with other objects in your world. It uses a minimal hierarchy to keep render costs low.
- Pose graph: A set of target poses defines key positions the character should reach. Each pose includes joint angles, limb positions, and orientation data.
- Motion controller: A simple controller advances from pose to pose using a blend factor and timing. It supports looping, ping-pong motion, and custom sequencing.
- Easing and timing: The system uses linear interpolation with easing curves. You can adjust durations, delays, and easing to shape the rhythm.
- Lighting and materials: The example scene uses standard materials with soft shadows to emphasize form. Lighting is kept adjustable so you can tailor mood without code changes.
- Input handling: The dancer responds to a few well-defined inputs, such as play/pause, speed adjustments, and pose overrides. You can wire your own controls to these inputs.

Getting started
- Prerequisites: Node.js and a package manager (npm or yarn). A modern browser with WebGL support is required for the demo.
- System requirements: A mid-range GPU can render the scene with reasonable frame rates. The demo scales down gracefully on devices with limited resources.
- Quick start path: You can try the example scene in the released assets. Download the release asset from the Releases section, extract it, and run the included start script. The release page contains a packaged version you can run without building from source.

Downloads and releases
- The official releases page contains the packaged assets you can run directly. From the Releases page, download the latest release asset (zip). Unpack it and follow the included instructions to start the demo. The linked page also hosts versioned builds you can compare as your scene evolves. For convenience, the same link is provided here: https://github.com/Khaionsen/r3f-character-dance/releases

- If you prefer building from source or exploring the code, you can fetch the repository from GitHub. The source provides the components and utilities used to render the dancer and orchestrate motion. The design encourages experimentation and rapid iteration.

Installation and setup
- Install the repository locally
  - Create a workspace for the project or open an existing one that can host a 3D demo.
  - Clone the repository:
    - git clone https://github.com/Khaionsen/r3f-character-dance.git
  - Navigate into the project directory:
    - cd r3f-character-dance
  - Install dependencies:
    - npm install
    - or yarn install
- Run the development server
  - Start the local dev server:
    - npm run dev
  - Open the local URL shown in the terminal to view the dancer in action.
- Build for production
  - Prepare a production build:
    - npm run build
  - Serve the built assets with a static server of your choice or host them in a web environment that supports static content.

Running locally
- Development workflow
  - The project uses hot module replacement to update code in real time as you tweak motion parameters.
  - Changes to the pose graph, durations, or easing curves reflect immediately in the running scene.
- Debugging tips
  - Check the console for warnings about shader compilation or missing textures. These messages guide you toward missing assets or misconfigured materials.
  - If the scene runs slowly on a target device, lower the resolution of textures or reduce the number of particles and mesh instances in the dance. The dancer works at multiple scales; you can adjust to fit the platform.

API and components
- CharacterDance component
  - Props
    - speed: number. Controls the overall tempo of the dance.
    - intensity: number. Scales the amplitude of limb motion.
    - loop: boolean. Enables continuous looping of the motion sequence.
    - onComplete?: () => void. Callback fired when a motion cycle finishes.
  - Behavior
    - The component attaches to a character mesh or group and applies pose transforms to limbs in a safe, reversible manner.
    - It blends current pose data with target pose data to produce smooth transitions.
- PoseTarget
  - Represents a specific arrangement of joints and bone orientations.
  - Used to define the key positions in the motion graph.
- MotionGraph
  - A lightweight graph that sequences poses and defines transitions.
  - Supports timing, repetition, and non-linear progressions.

Usage examples
- Basic usage with a stand-in character
  - import { CharacterDance, PoseTarget, MotionGraph } from 'r3f-character-dance';
  - const danceGraph = new MotionGraph([
      new PoseTarget('start', { hips: 0.0, leftArm: 0.0, rightArm: 0.0 }),
      new PoseTarget('raise', { hips: 0.1, leftArm: 0.9, rightArm: -0.9 }),
      new PoseTarget('spin', { hips: 0.0, twist: 1.0 }),
    ]);
  - <CharacterDance speed={1.0} intensity={1.0} loop={true} graph={danceGraph} />

- Type-safe example in TypeScript
  - interface DancerProps {
      speed: number;
      intensity: number;
      loop?: boolean;
    }
  - const Dancer: React.FC<DancerProps> = ({ speed, intensity, loop = true }) => (
      <CharacterDance speed={speed} intensity={intensity} loop={loop} />
    );
  - export default Dancer;

- Advanced usage with custom shaders and materials
  - The project exposes hooks to override materials or provide custom shaders. You can plug in your own shader passes to achieve unique glow effects, rim lighting, or stylized outlines that respond to the dancer’s motion.
  - For example, you can inject a post-process stage to enhance edges during key poses and soften the silhouette during idle sections.

Customization and theming
- Color and lighting
  - The scene uses a standard lighting setup, with a key light and fill light to create depth. You can adjust the light color, intensity, and position to match your project’s mood.
  - Materials support basic properties like color, roughness, and metalness. You can tailor these to get a glossy, matte, or metallic look on the character model.
- Motion styling
  - The motion graph supports custom easing curves for each transition. Use simple linear, cubic, or quintic curves to shape the speed profile of each move.
  - Tempo can be changed dynamically at runtime to reflect in-scene cues or user input.
- Character rig support
  - The dancer is designed to work with typical humanoid rigs. If you have a custom rig, you can adapt the pose targets to match the bone layout.
  - In most cases, you only need to map the high-level pose positions to your rig’s bones. The system does not rely on a fixed mesh topology.

Animations and motion details
- Pose design
  - Poses are defined as a set of bone rotations and joint angles. Each pose targets a distinct moment in the dance sequence.
  - A pose can emphasize balance, reach, or rotational movement. By combining poses, you can create a narrative arc in the dance.
- Transitions
  - Transitions are blended over a fixed duration. You can adjust the transition time to make moves feel snappier or smoother.
  - Non-linear pacing adds personality. Short, sharp transitions produce a salsa-like energy; longer blends produce a lull between moves.
- Rhythm and timing
  - Rhythm is a core part of the dance. The tempo prop controls the speed of the entire sequence.
  - You can synchronize the dance with audio or other scene events by aligning the tempo and transition timing with the beat.

Scene composition
- Environment setup
  - A minimal environment helps the dancer pop visually. Use a simple ground plane, subtle ambient light, and a distant horizon to create depth.
  - Shadows add realism; enable soft shadows and adjust the shadow bias to reduce artifacts.
- Camera and perspective
  - A dynamic camera can follow the dancer, rotate around the character, or switch between preset views.
  - The camera should not overpower the motion. A gentle motion or a fixed, cinematic angle often works best for showcasing the dance.

Assets and releases
- Release assets
  - The release bundle includes a ready-to-run scene with a complete dancer, a small set of props, and a runnable demo. The asset package is designed for quick onboarding and easy modification.
  - After downloading the latest release asset, follow the instructions included in the bundle to start the demo. The asset includes a preconfigured scene, a basic UI for playback, and a few example props to illustrate how the dancer interacts with the environment.
- Asset structure
  - The assets folder contains models, textures, and materials used in the demo.
  - A separate shaders folder houses a couple of example shader programs.
  - A data folder holds the pose targets, motion graph definitions, and a tiny utility library used to validate animations.
- Extending assets
  - If you want to add additional assets, keep the structure consistent. Place new models under assets/models, textures under assets/textures, and materials under assets/materials.
  - Update the motion graph with new poses by adding new PoseTarget instances and extending the transitions.

Development workflow
- Code organization
  - The codebase is organized into a small set of focused modules. Each module has a clear responsibility: scene setup, dancer logic, pose data, and utilities.
  - The separation makes it easier to reuse the dancer in other scenes without dragging along unrelated logic.
- Type safety and linting
  - TypeScript is used to prevent type errors. Interfaces describe the shape of pose data and props for components.
  - A lightweight lint setup helps maintain code quality and consistency across contributors.
- Testing approach
  - Visual tests are partially manual by design. You can verify motion by running the demo in a browser and visually inspecting the animation.
  - If you want automated checks, consider snapshot testing of the component tree and a few unit tests for the motion graph logic.

Testing and quality
- Visual validation
  - Run the demo in different browsers and devices to confirm rendering consistency and motion stability.
  - Observe how lighting interacts with the model during key poses and transitions.
- Performance profiling
  - Use browser performance tools to measure frame times during busy scenes.
  - Identify bottlenecks, such as high-polygon meshes or excessive texture sizes, and reduce them for smoother playback.
- Accessibility checks
  - Ensure controls are reachable via keyboard or accessible UI components.
  - Provide alt text or descriptive labels for any on-screen controls to improve screen reader compatibility.

Accessibility and usability
- Keyboard controls
  - Space toggles play/pause.
  - Arrow keys adjust tempo and intensity, allowing quick experimentation during live coding sessions.
- UI clarity
  - The on-screen UI uses clear labels and big tappable areas to improve usability on touch devices.
  - Feedback messages appear when actions are performed, such as pose changes or tempo adjustments.

Performance considerations
- Rendering efficiency
  - Use instanced meshes or lightweight geometry when possible to keep the draw calls low.
  - Minimize state changes in the WebGL pipeline to avoid costly GPU switches.
- Resource management
  - Reuse materials and textures where possible.
  - Pool small objects and keep the scene graph shallow to reduce update overhead.

Debugging tips
- Common issues
  - The dancer remains static: verify that the motion graph has at least two poses and that the play state is active.
  - Animations look wrong: check that the pose targets align with the rig and that the bone mapping matches the model.
  - Lighting looks harsh: adjust the key light direction and color to achieve a pleasing mood.
- Helpful diagnostics
  - Print pose indices as the dancer transitions to ensure transitions occur in the expected sequence.
  - Log the current tempo and intensity for quick feedback during live tweaking.

Examples and patterns
- Simple scene
  - A small scene with a single dancer, a ground plane, and three lights to highlight form.
- Multi-character scene
  - Expand to two or more dancers sharing the same motion graph or each using its own graph for synchronized or contrasting choreography.
- Interactive scene
  - Allow users to influence tempo and pose by dragging sliders or moving a cursor. The dancer responds in real time with smooth interpolation.

Contributing
- How to contribute
  - Start by forking the repository and creating a feature branch for your changes.
  - Keep changes focused and small. Propose a single improvement per commit.
  - Add tests or visual checks where feasible. Document your changes in a concise manner.
- Code style
  - Follow the existing code style. Use descriptive names for variables and functions.
  - Write small, well-scoped functions with a single responsibility.
- Review process
  - Submit a pull request with a clear description of the change, its purpose, and its impact on the dancer system.
  - Be prepared to respond to feedback and iterate on the implementation.

Roadmap
- Short-term goals
  - Add more pose targets to enrich the motion graph.
  - Improve UI to better reflect the dancer's rhythm and energy levels.
  - Introduce a simple preset system for common dance styles.
- Medium-term goals
  - Support more rig configurations, including facial expressions for stylized animation.
  - Enable runtime shader customization to experiment with different visual styles.
  - Build a small gallery of scenes that demonstrate the dancer in varied environments.
- Long-term goals
  - Publish a polished npm package with a clean API for easy integration into new projects.
  - Create a collection of fiction and non-fiction motion sequences that educators can use to teach timing and rhythm.

License and credits
- License
  - This project is released under the MIT License. See LICENSE for details.
- Credits
  - The dancer is built with React Three Fiber and Three.js contributions in mind. Thanks to the community for ongoing performance improvements and shader techniques.
- Acknowledgments
  - Special thanks to the open-source ecosystem for the tools and ideas that make this project possible. The collaboration between web graphics and interactive art yields engaging experiments.

FAQ
- What is r3f Character Dance?
  - It is a small, experiment-friendly motion system that showcases a character performing choreographed moves using React Three Fiber.
- Can I use this in my own project?
  - Yes. The design is modular and easy to integrate into a variety of scenes, from demos to serious apps.
- Do I need a strong GPU to run this?
  - A mid-range GPU is enough for a pleasant experience. You can scale down assets and textures to fit lower-end hardware.
- How do I customize the motion?
  - You modify the pose targets and transition timings. The motion graph will blend poses to produce the final motion.

Notes on safety and reliability
- The dancer is designed to be safe to run in typical browser environments. If you deploy this in a production setting, ensure you follow standard security practices for JavaScript-based projects, including dependency updates and secure hosting.
- The codebase remains small on purpose. The small footprint makes it easier to audit and understand. If you want to extend, start with a single module and add tests as you go.

Visual references and imagery
- Visual style is inspired by real-time 3D performance pieces. The aesthetic aims for clean geometry, clear silhouette, and crisp shading, with a focus on readability of motion.
- If you need reference imagery, you can search for motion capture-inspired visuals, stage lighting concepts, and character rig illustrations to guide your own design decisions.

Appendix: Project structure at a glance
- src/
  - dancer/
    - CharacterDance.tsx
    - PoseTarget.ts
    - MotionGraph.ts
  - scene/
    - SceneSetup.tsx
    - Lighting.tsx
  - utils/
    - easing.ts
    - poseUtils.ts
- public/
  - index.html
  - assets/
    - models/
    - textures/
- tests/
  - dancer.test.ts
- README.md
- package.json
- tsconfig.json

End note
- The path to the release file and assets is accessible on the Releases page linked above. The same link is used here to direct you to the source of packaged content, and it serves as the primary gateway for obtaining stable, tested builds that you can run directly.

