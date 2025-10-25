# CreateLightCookie
Landing page for [Create Light Cookie](https://assetstore.unity.com/packages/slug/339304) on the Unity Asset Store. 

--- 

> [!IMPORTANT]
> The contents of this ReadMe do not provide, modify, renew or change any licensure for the Create Light Cookie asset.

# Auto Light Cookie Generator
**Version:** 1.0  
**Author:** Void Wire Interactive  
**Unity Compatibility:** 2022.3 LTS and later (including Unity 6.x)  
**Category:** Lighting / Editor Tools  

---

## Quick Start

1. **Installation location of assets**
   - Copy the following files into your Unity project:
     ```
     Assets/VoidWireInteractive/AutoLightCookie/Scripts/Editor
     ├── ALC_Light.cs
     └── ED_BatchCubemapCookiesFromProbes.cs
     └── ED_ALC_LabelContents
     
     Assets/VoidWireInteractive/AutoLightCookie/Prefabs
     └── InvertedNormals_Sphere
     
     Assets/VoidWireInteractive/AutoLightCookie/Demo
     └── AutoLightCookie_DemoScene
     ```
2. **Open the Tool**
   - In Unity, go to:  
     - For Geometry Based: **Tools → Void Wire Interactive → Lighting → Auto Light Cookie → Generate From Geometry**
     - For Procedurally Based: **Tools → Void Wire Interactive → Lighting → Auto Light Cookie → Generate Procedural**

3. **Select Lights**
   - In the Hierarchy, select one or more **Point** or **Spot** lights.

4. **Configure Settings**
   - Adjust resolution, save path, and optional preview controls.

5. **Generate**
   - Click **Generate and Assign Cookies** to automatically bake and assign cookies.

6. **Preview & Fine Tune**
   - Enable **Override Exposure** to interactively preview or adjust contrast and ranges.

7. **Save**
   - Apply and save your cookies. Assets are stored in your project folder and assigned automatically to each light.

---

## Overview

The **Auto Light Cookie Generator** automates the creation of **realistic light cookies** for both **Point Lights** and **Spot Lights** directly within the Unity Editor.

This system captures the light’s visual contribution using **Reflection Probes** (for Point Lights) or **Cameras** (for Spot Lights), converts the data to grayscale cookies, and applies them to the corresponding lights.  

These cookies enhance lighting contrast, volume definition, and shadow realism without requiring manual texture authoring.

---

## Features

### General
- Supports **Point Lights (Cubemap cookies)** and **Spot Lights (2D cookies)**.
- Batch generation for multiple selected lights.
- Interactive, resizable in-editor preview.
- Real-time exposure, brightness, and contrast control.
- Automatic grayscale normalization.
- Persistent asset tracking through `ALC_Light` component.
- Auto-import of generated EXR and PNG assets.
- Saves cookies directly into your project and links them to the lights.

---


The EditorWindow provides the main interface for generating, previewing, and managing cookies.

#### Menu Path
Tools → Void Wire Interactive → Lighting → Generate From Geometry

#### Supported Light Types
- **Point Light:** EXR Cubemap Cookie generated via Reflection Probe.
- **Spot Light:** PNG 2D Cookie generated via temporary Camera capture.

--- 
</b>

# Geometry Based Generator Usage Guide

### Step 1. Open the Generator
- Access the generator via **Tools → Void Wire Interactive → Lighting → Generate From Geometry**.
- ![alt text](https://github.com/VoidWireInteractive/CreateLightCookie/blob/main/GeometryInterface.png "StartingInterface")

### Step 2. Select Lights
- Select one or more **Point** or **Spot** lights from the Hierarchy.

### Step 3. Configure Settings

#### For Point Lights
| Setting | Description |
|----------|--------------|
| **Cubemap Resolution** | Output size: 128, 256, 512, or 1024. |
| **Save Path** | Folder path for generated EXR cookies. |
| **Override Exposure** | Enables advanced preview controls. |
| **Auto Update Preview** | Automatically updates the preview in real-time. |
| **Use Ranges** | Enables black and white value control for specific sets of pixels between or within chosen black/white ranges. |
| **Darkness/Lightness Multipliers** | Adjust intensity and brightness levels. |
| **Contrast** | Controls preview and saved contrast intensity. |

#### For Spot Lights
| Setting | Description |
|----------|--------------|
| **Spot Cookie Resolution** | Texture resolution: 256, 512, 1024, or 2048. |
| **Save Path** | Folder path for generated PNG cookies. |
| **Override Exposure** | Enables preview adjustment settings. |
| **Auto Update Preview** | Updates preview dynamically as sliders change. |
| **Use Ranges** | Enables range-based value clamping and scaling. |


### Override Functionality
#### Non Range adjustments
![alt text](https://github.com/VoidWireInteractive/CreateLightCookie/blob/main/GeoNonRange.png "Override Settings Non Ranged")
 - **Midpont Threshold:** Determining factor for what is considered light and dark. Anything less than this value is considered darkness where as above is lightness.
 - **Darkness Multiplier:** Multiplies the darkness value of a pixel below the set threshold
 - **Lightness Multiplier:** Multiplies the lightness value of a pixel above the set threshold
 - **Contrast:** Light/Dark Emphasis
---
#### Ranged adjustments
![alt text](https://github.com/VoidWireInteractive/CreateLightCookie/blob/main/GeoRange.png "Override Settings Ranged")
 - **Darkness Multiplier:** Multiplies the darkness value of a pixel below the set threshold
 - **Lightness Multiplier:** Multiplies the lightness value of a pixel above the set threshold
 - **Contrast:** Light/Dark Emphasis
 - **Ranges Behavior:**
    - **Between Is Multiplied:** Any pixel that falls within the selected ranges is multiplied by the allocated light/dark multipliers. The outliers are left unmodified 
    - **Outside Is Multiplied:** The inverse of the between is multiplied option. Pixels that fall outside the ranges are multiplied whereas the pixels within are left unmodified.
    - **Clamp Outliers To Ranges:** Clamp pixel values, that fall outside the selected ranges, to the highest or lowest bound of the nearest range available.
 - **MidRanges Behavior:**
    - **None**: Nothing is altered
    - **Lerp to Closest:** Interpolates to the closest range bound. ex: if darknessRange.upperBound = '0.3' & lightnessRange.lowerBound = '0.9' and the pixelValue = '0.4'. the midPoint of the bounds is '0.6'. The resulting pixel value will be '0.333~'
    - **Clamp to Closest:** The pixel value will be forced to whichever bound is closest between darknessRange.upperBound & lightnessRange.lowerBound.
    - **Apply Multipliers:** The pixel value will simply be multiplied by the darkness/lightness multiplier values
---

### Step 4. Generate Cookies
Click **Generate and Assign Cookies** to:
- Create cookie assets for all selected lights.
- Automatically add the `ALC_Light` component if missing.
- Assign cookies directly to the light’s **Cookie** property.
- Save cookies to the designated output folder.

---

### Step 5. Preview and Adjust
When **Override Exposure** is enabled:
- Adjust **Darkness Range**, **Lightness Range**, **Threshold**, and **Contrast** interactively.
- Apply changes using **Apply Changes to Preview**.
- Permanently update assets using **Apply & Save To Cookie**.
- Revert all parameters with **Revert to Default**.

A live preview is shown at the bottom of the window.  
You can drag the upper bar to resize the preview area.

---

### Step 6. Apply Last Generated
If a light already has previously generated data, use **Apply Last Generated** to re-apply or update the existing cookie without baking again.

---
## Button Assignments
- **Generate and Assign Cookies**: [Destructive] Saves or Overwrites the current allocated texture for the light cookie. This is destructive if a cookie already exists under the same name. 
- **Apply Last Generated**: If a set of values for the currently selected object can be found, they can be reloaded from their most recent generation.
- **Apply Changes To Preview**: If the `Auto Update Preview` is `false`, this applies the current settings to the preview window texture.
- **Rever To Default**: Resets the values of the window to default.

---

## Technical Implementation

### Point Light (Cubemap Cookie)
- A temporary **Reflection Probe** is spawned at the light’s position.
- The probe captures an EXR cubemap from the environment.
- The cubemap is desaturated and normalized.
- The EXR is imported as a Cubemap asset and assigned to the light’s **cookie** field.

### Spot Light (2D Cookie)
- A temporary **Camera** is created and aligned to the light.
- The camera renders the scene to a RenderTexture.
- The texture is desaturated and normalized.
- The final PNG is saved, imported, and assigned as the light’s cookie.

---

## Output Files

| Light Type | File Format | Example Name | Output Folder |
|-------------|-------------|---------------|----------------|
| Point Lights | `.exr` | `[lightObjectName]_[lightTransformInstanceId]_genCookie.exr` | `Assets/VoidWireInteractive/AutoLightCookie/CookieOutputs/` |
| Spot Lights | `.png` | `[lightObjectName]_[lightTransformInstanceId]_genCookie.png` | `Assets/VoidWireInteractive/AutoLightCookie/CookieOutputs/` |

---

## Notes and Recommendations
- Generated assets must have **Read/Write Enabled** for previewing; the tool temporarily enables and disables this flag automatically.
- If using **HDRP**, ensure Reflection Probes and mixed lighting are properly configured.
- Point Light generation may take longer due to reflection probe baking.
- Always maintain a clean save path for consistent asset references.

---

## Troubleshooting

| Issue | Cause | Solution |
|-------|--------|----------|
| Cookie appears black or overexposed | Lighting intensity or exposure imbalance | Enable Override Exposure and adjust brightness/contrast |
| EXR import fails | Asset not imported as Cubemap | Re-run generation or set TextureImporter type to Cubemap |
| Spot cookie looks flipped | Incorrect light rotation | Verify the Spot Light’s transform orientation |
| Reflection probe fails | Scene lighting data not baked | Update lighting and retry generation |
| Generated Textures Show albedo details of light blocking objects | Render shadows only on nearby meshes not set correctly | Delete the generations and attempt to generate again |

---

--- 
</b>

# Procedurally Based Generator Usage Guide

### Step 1. Open the Generator
- Access the generator via **Tools → Void Wire Interactive → Lighting → Generate Procedural**.
- ![alt text](https://github.com/VoidWireInteractive/CreateLightCookie/blob/main/ProcGenInterface.png "StartingInterface")

### Step 2. Select Light
- Select one **Spot** light from the Hierarchy.

### Step 3. Configure Settings
---
#### Presets
 - These presets will be allocated via `Scriptable object` if you so choose to create one using the **Is New Preset** options. The data used will persist as a scriptable object `Assets/VoidWireInteractive/AutoLightCookie/Presets/2d Large Spotlight Cookie.asset`

#### Pattern Types
| Pattern | Properties |
|-------------|-------------|
| Radial | `Falloff`  |
| Lens | `Lens Radius`, `Ring Frequency`, `Distortion Strength`, `Falloff`, `High Noise Scale`, `Low Noise Scale`, `Blend Bias` |
| Perlin Noise | `Noise Scale` |
| Caustics | `Noise Scale`, `Intensity`, `Time`, `Time Offset X`, `Time Offset Y`, `Ripples`, `Undulations`, `Vertical Distortion` |
| Grid | `Vertical Lines`, `Horizontal Lines` |
| Slits | `Slit Width`, `Slit Count` |
| Random Mask | `Mask Density` |

#### Property Definitions
   - **Falloff**: Controls the rate at which the radial pattern fades from center to edge. Effectively controls how fast the brightness fades from center to edge.
   - **Lens Radius**: Controls the radius of the lens effect in the procedural pattern.
   - **Ring Frequency**: Determines the frequency of the rings in the radial pattern.
   - **Distortion Strength**: Adjusts the strength of the distortion applied to the procedural pattern. 
   - **High Noise Scale**: Adjusts the scale of the secondary high-frequency noise pattern.
   - **Low Noise Scale**: Adjusts the scale of the primary low-frequency noise pattern.
   - **Blend Bias**: Adjusts the bias of the blending between the two noise patterns.
   - **Noise Scale**: Adjusts the scale of the Perlin noise pattern.
   - **Intensity**: Adjusts the intensity of the caustic noise pattern.
   - **Time**: Adjusts the simulated time of the caustics pattern.
   - **Time Offset X**: Slightly offsets the x-direction wave animation from the base
   - **Time Offset Y**: Slightly slows or speeds the vertical/time component of wave
   - **Ripples**: Controls fine vs coarse ripples
   - **Undulations**: Introduces gentle broad undulations on top of fine ripples. Essentially would be like big slow waves.
   - **Vertical Distortion**: Breaks symmetry between x and y, adds complexity to pattern
   - **Vertical Lines**: Determines the number of lines in the grid pattern.
   - **Horizontal Lines**: Determines the number of lines in the grid pattern.
   - **Slit Width**: Controls the width of the slits in the pattern.
   - **Slit Count**: Controls the number of slits in the pattern.
   - **Mask Density**: Adjusts the density of the random mask pattern.
---

## Button Assignments
- **Save Current As New Preset**: Creates a new preset under `Assets/VoidWireInteractive/AutoLightCookie/Presets/[name].asset` for the current allocated values.
- **Generate Light Cookies**: [Destructive] Saves or Overwrites the current allocated texture for the light cookie. This is destructive if a cookie already exists under the same name.
- **Set Default Values**: Resets the values of the window to default.
- **Load Previous Values**: If a set of values for the currently selected object can be found, they can be reloaded from their most recent generation.

## License and Support

**Copyright 2025 © Void Wire Interactive**  
This software is proprietary and may not be redistributed or modified without explicit permission.

---

## Changelog
**v1.0**
- Initial release  
- Added support for Point and Spot Light cookie generation  
- Real-time preview with adjustable exposure and contrast  
- Batch selection support  
- Auto asset management and import configuration  

---

