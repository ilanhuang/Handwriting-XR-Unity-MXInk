# HandwritingXR MX Ink Setup Guide

## Description
- This is a prototype that integrates Logitech's MX Ink stylus with Unity XR Interaction toolkit to enable handwriting input, which is captured as stroke data using a modified LineDrawing system from Logitech's MXInk Unity Integration sample. The MxInkHandler manages stylus interactions, while the HandwritingXR component processes and exports the strokes. The strokes are then sent to MyScriptAPI, which converts them into digital text using handwriting recognition. Finally, the recognized text is displayed on a Unity Canvas with TextMeshPro (TMP) via the TextManager.

## Notice:
- This prototype comes from a previous one that tracks a fingertip to create handwriting inputs. You can find more info here: https://github.com/ilanhuang/Handwriting-XR-Unity
- This prototype uses a modified version of LineDrawing script from the Logitech's MXInk Unity support with OpenXR. You can find more info here: https://logitech.github.io/mxink/UnityIntegration.html
- To recreate this prototype you will need a MyScript developers account. You can sign up for it here: https://developer.myscript.com/

## Setup Instructions

1. **Create a new Unity project** (Unity 6 recommended).
2. **Enable OpenXR** for Windows and Android in **Project Settings**, then fix any issues in **Validation**.
3. **Install required packages** from the **Package Manager**:
   - **XR Interaction Toolkit 3.0** + **Starter Assets Sample** (for XR Origin)
   - **Newtonsoft Json** package
4. **Import the `HandwritingXR-MXInk` Unity package.** (You may need to fix validation issues again.)
5. **Set up the XR Origin**:
   - In the **Sample Scene**, delete the **Main Camera**.
   - Drag the **XR Origin** prefab from **Starter Assets Sample** into the scene.
6. **Add the MX Ink stylus**:
   - Go to the **Logitech** folder in **Prefabs** (imported from the package).
   - Drag and drop the **MX Ink** prefab inside **Camera Offset** (inside XR Origin).
   - Inside the MX Ink prefab, you will find **Right Hand** and **Left Hand** stylus parent objects. **Activate the one you wish**.
   - Inside these objects, you will find the stylus models.
   - (Optional) Change the **Motion Controller** in XR Origin’s **XR Input Modality Manager** to the stylus to avoid controller-stylus overlap.
7. **Add the Canvas for displaying text**:
   - Drag and drop the **Canvas** prefab from the **HandwritingXR** folder (imported from the package) into the scene.
8. **Set up the HandwritingXR system**:
   - Create an empty **parent GameObject** called `HandwritingXR`.
   - Attach the following components (scripts) found inside the **HandwritingXR** folder:
     - `HandwritingXR` (from **src** folder)
     - `TextManager` (from **utils** folder)
     - `MyScriptAPI` (from **services** folder)
9. **Create the MyScriptAPI settings**:
   - Right-click inside the **services** folder and create a **MyScriptAPISettings** Scriptable Object.
10. **Set up MyScript API**:
    - Create a **developer account** on **MyScript** and verify it to access the **Cloud Recognition Console**.
    - Create a **new app** and go to the **Key section**.
    - Populate the **MyScriptAPISettings** Scriptable Object with:
      - **Application Key** (from MyScript)
      - **HMAC Key** (from MyScript)
      - **API URL**: `https://cloud.myscript.com/api/v4.0/iink/batch`
11. **Connect the LineDrawing system**:
    - Drag the **LineDrawing** prefab from **Logitech’s Prefabs folder** into the `HandwritingXR` parent object.
    - Drag the **stylus** (either left hand or right hand) from **MX Ink inside Camera Offset** into the **Stylus field** of `LineDrawing`.
12. **Finalize component assignments**:
    - Drag the **TMP object inside Canvas** into the **TextManager** component field.
    - Assign the **MyScriptAPISettings** Scriptable Object (created in step 9) to the **MyScriptAPI** component.
    - Drag and drop the following into their respective fields in the **HandwritingXR** component:
      - **LineDrawing**
      - **MX Ink stylus** (same as step 11)
      - **TextManager**
      - **MyScriptAPI**

---

## To-Do's
-As this is just a fast prototype there are a lot of things to polish if production usage is intended.

1. Work in the strokes capturing logic as for now, each word must be written in a single stroke which can be counter intuitive. 

