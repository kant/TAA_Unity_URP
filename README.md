# Temporal Anti-Alasing for Unity’s Universal Render Pipeline

This Temporal Anti-Aliasing package provides full object motion blur for Unity's Universal Render Pipeline. It jitters the camera's projection before the whole rendering process, , which can samples differant surface between adjacent frames. Temporal Anti-Aliasing can then be enabled with the provided **Temporal Anti-Aliasing** **Volume Component** for Scriptable Render Pipeline's **Volume** system, supported by default in Universal Render Pipeline.

## Instructions
- Open your project manifest file (`MyProject/Packages/manifest.json`).
- Add `"com.xienaiwen.taa": "file:src/NaiwenTAA",` to the `dependencies` list.
- Open or focus on Unity Editor to resolve packages.
- Enable "Depth Texture" in the pipeline asset.
- Add TAAFeature in the render's asset settting.
![Add_Features.png](https://github.com/sienaiwun/publicImgs/blob/master/imgs/TAA/Add_Features.png?raw=true)
- Add "Temporal Anti-Aliasing" Component in the Post-process Vilome and set the "feedback" param to more than 0.
![Post-process%20Volumn.png](https://github.com/sienaiwun/publicImgs/blob/master/imgs/TAA/Post-process%20Volumn.png?raw=true)

## Requirements
- Unity 2019.3.0f3 or higher.

## Why 
Unity's default Temporal Anti-Aliasing(TAA) has some problems in Universal Render Pipeline (URP). Natively, URP does not support TAA while Unity PostProcess V2 does support. However, PostProcess V2's support fails for TAA because it cannot jitter the camera in the ScriptableRenderPipeline [PostProcessLayer.cs] line:996(https://github.com/Unity-Technologies/PostProcessing/blob/v2/PostProcessing/Runtime/PostProcessLayer.cs)
In the Frame Analysis, we also find there is no jitter in the native PostProcess V2 TAA pass.

![TAA_PP_Failed](https://github.com/sienaiwun/publicImgs/blob/master/imgs/TAA/TAA_PP_Failed.png?raw=true)

## Result
![NOAA.png](https://github.com/sienaiwun/publicImgs/blob/master/imgs/TAA/NOAA.png?raw=true)
TAA:

![TAA.png](https://github.com/sienaiwun/publicImgs/blob/master/imgs/TAA/TAA.png?raw=true)

FXAA:

![FXAA.png](https://github.com/sienaiwun/publicImgs/blob/master/imgs/TAA/FXAA.png?raw=true)

MSAA2x:

![MSAA2x.png](https://github.com/sienaiwun/publicImgs/blob/master/imgs/TAA/MSAA2x.png?raw=true)

MSAA4x:
![MSAA4x.png](https://github.com/sienaiwun/publicImgs/blob/master/imgs/TAA/MSAA4x.png?raw=true)