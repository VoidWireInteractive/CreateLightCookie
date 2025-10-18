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
     **Tools → Void Wire Interactive → Lighting → Batch Generate Light Cookies**

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
Tools → Void Wire Interactive → Lighting → Batch Generate Light Cookies

#### Supported Light Types
- **Point Light:** EXR Cubemap Cookie generated via Reflection Probe.
- **Spot Light:** PNG 2D Cookie generated via temporary Camera capture.

---

## Usage Guide

### Step 1. Open the Generator
- Access the generator via **Tools → Void Wire Interactive → Lighting → Batch Generate Light Cookies**.

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
| **Use Ranges** | Enables black and white value control. |
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

