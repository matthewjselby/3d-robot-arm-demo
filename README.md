# 6-DOF Robotic Arm Demo

An interactive 3D simulation of a 6-axis robotic arm built with Three.js. This demo features real-time kinematics, collision detection, and an intuitive control interface.

## Features

### Six Degrees of Freedom

The robotic arm includes six independently controllable joints:

- **J1: Base Rotation** (-180° to 180°) - Rotates the entire arm around the vertical axis
- **J2: Shoulder** (-90° to 90°) - Controls the angle of the upper arm
- **J3: Elbow** (-135° to 135°) - Adjusts the forearm position
- **J4: Wrist Roll** (-180° to 180°) - Rolls the wrist along the arm's axis
- **J5: Wrist Pitch** (-90° to 90°) - Pitches the end effector up and down
- **J6: Wrist Yaw** (-180° to 180°) - Rotates the end effector left and right

### Interactive Controls

- **Slider Controls**: Adjust each joint angle with precision using responsive sliders
- **Real-time Feedback**: Joint angles displayed in degrees with live updates
- **Reset Button**: Returns the arm to its default pose with smooth animation
- **Mouse Camera Control**: Rotate, pan, and zoom the 3D view using mouse or trackpad

### Collision Detection

The simulation includes intelligent collision avoidance:

- **Ground Plane Detection**: Prevents the arm from intersecting the floor
- **Base Collision**: Avoids self-collision with the base platform
- **Automatic Reversion**: Invalid movements are automatically prevented, and joints revert to safe positions
- **Safety Margins**: Built-in clearance zones ensure realistic operation

### Modern UI Design

- **Custom Fonts**: Uses Orbitron and JetBrains Mono for a technical look
- **Animated Grid Background**: Subtle grid pattern creates depth
- **Smooth Animations**: Eased transitions for preset poses
- **Responsive Layout**: Adapts to different screen sizes

### Advanced Rendering

Built with Three.js, featuring:

- **Realistic Lighting**: Directional, ambient, point, and fill lights for depth
- **Dynamic Shadows**: Real-time shadow mapping with PCF soft shadows
- **Metallic Materials**: PBR materials with varying roughness and metalness
- **Emissive Effects**: Glowing joints and end effector
- **Fog Effect**: Atmospheric perspective for realism

## Technical Details

### Architecture

The robotic arm is constructed using a hierarchical joint structure where each joint is a child of the previous one:

```
Base (fixed)
└── J1 (Base Rotation)
    └── J2 (Shoulder)
        └── J3 (Elbow)
            └── J4 (Wrist Roll)
                └── J5 (Wrist Pitch)
                    └── J6 (End Effector)
```

### Collision System

The collision detection system samples multiple points along the arm segments and checks their positions against:
- Ground plane (Y < 0.15m with safety margin)
- Base cylinder (radius 1.5m, height 0.5m with safety margin)

When a collision is detected, the last joint movement is immediately reverted to the previous safe state.

### Animation System

Preset poses use cubic ease-in-out interpolation for smooth, natural-looking movements. The animation system updates all six joints simultaneously while continuously checking for collisions.

## Usage

### Getting Started

Simply open `index.html` in a modern web browser. No build process or dependencies to install - everything is self-contained using CDN imports.

### Controls

1. **Adjust Joints**: Drag the sliders in the control panel to move individual joints
2. **Rotate View**: Click and drag on the canvas to orbit the camera
3. **Zoom**: Scroll or pinch to zoom in/out
4. **Pan**: Right-click and drag (or two-finger drag) to pan the camera
5. **Reset**: Click the "Reset" button to return to the default pose

### Browser Requirements

- Modern browser with WebGL support
- JavaScript enabled
- Recommended: Chrome, Firefox, Safari, or Edge (latest versions)

## Code Structure

### HTML Structure

- `#canvas-container`: WebGL renderer canvas
- `#controls`: Right-side control panel with joint sliders
- `#info`: Bottom-left information panel

### JavaScript Modules

- **Scene Setup**: Camera, renderer, lighting, and environment
- **Arm Construction**: Hierarchical joint and link creation
- **Control System**: Slider event handlers and joint updates
- **Collision Detection**: Ground and base intersection testing
- **Animation**: Smooth interpolated transitions

### Styling

CSS custom properties define the color scheme:
- `--bg-dark`: Main background
- `--bg-panel`: Control panel background
- `--accent-cyan`: Primary accent color
- `--accent-orange`: Secondary accent color
- `--text-primary`: Main text color
- `--text-dim`: Secondary text color

## Performance

The demo runs at 60 FPS on modern hardware with:
- Optimized collision checking (minimal sample points)
- Efficient shadow mapping (2048x2048 resolution)
- Damped camera controls for smooth interaction
- Conditional rendering updates

## Customization

### Modifying Joint Ranges

Edit the `min` and `max` attributes on range inputs:

```html
<input type="range" id="j2" min="-90" max="90" value="20" step="1">
```
