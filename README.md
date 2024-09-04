# ISH3DE: Intuitive Stereoptic Haptic 3D Data Exploration

## Overview

ISH3DE is a multisensory (multiple senses) extended reality (XR) applicaiton that supports image analysis and exploration for volumetric (bio-)medical images.
We performed a first evaluation on the usefulness of the software and published it as [journal paper](https://link.springer.com/article/10.1007/s10278-024-01094-x).
The version that was used for the evaluation is tagged with `studyversion2024`. 
In this version you can visually and haptically explore upper torso data from a CT scan that is part of the MedShapeNet collection.
If you want to try out this version or replicate the study, please use the corresponding readme file for setting up the project accordingly.

## Requirements

### Hardware

1. HTC Vive Pro 2 Full Kit: 
    - HTC Vive Pro 2 VR-Headset
    - 2 Basestations properly set up according to HTC Vive's information
    - 2 Controller 
    - 2 **additional** HTC Vive Tracker (we used version 3.0)
    - (it might also run with other VR-Headsets compatible with SteamVR, but this was not tested yet)

2. haptic glove of the company SenseGlove
    - We tested the software with SenseGlove DK1 or SenseGlove Nova (it may also run with SenseGlove Nova 2, but this was not tested yet).
    - attach the HTC Vive Tracker to the haptic gloves

3. Workstation or Laptop that is VR-ready, has bluetooth, and fullfills the requirements for the HTC Vive Pro 2.

### Software

This explanation is done for a Windows setup. 

1. SteamVR (to run the HTC Vive Pro 2 Set)
    - install driver [official software](https://www.vive.com/de/setup/vivepro2/)
    - Install SteamVR: 
      - install Steam -> Login -> install SteamVR  
      - on Windows: install ViveConsole (if not included in the package above)

2. SenseCom (server for SenseGloves DK1 and Nova)
    - can be found in their github repo [SenseGlove API](https://github.com/Adjuvo/SenseGlove-API/)

3. Unity
    - install latest Unity Hub
    - install Unity Version 2021.3.16f (Long-term-Support Version)

### Further Requirements

At least a 2m x 2m free space.

## Setup Instructions

This project includes custom scripts and scenes developed for ISH3DE. 
Some third-party assets are required for full functionality. 
Other third-party assets are just for creating a visually more appealing environment, and therefore, explicitely marked as *optional*.
If you want to replicate the study and use the scenes of the ISH3DE unitypackage, please download the optional third-party assets as well.

**Please follow the provided setup order and ensure that the package of this repository is included after the third-party assets and packages!!** 
Otherwise the dependencies will not be recognized properly.

1. **Create a new Unity project**:

2. **Import Required Custom Third-Party Unity Packages**:
    - SenseGlove API which can be found here [git](https://github.com/Adjuvo/SenseGlove-Unity)
      - Download it from the repository.
      - Open your Unity project and go to `Assets > Import Package > Custom Package...`, select the package and import it OR doubleclick the unitypackage in the Windows Explorer.
    - A modified version of an STL reader which can be found here: [git](https://github.com/JohnGames/pb_Stl)
      - Download it and place it in the folder *Packages*. 
      - (You can follow the readme for setting it up correctly, **BUT ensure to use the CORRECT url** not the one provided in the readme as it points to the not modified, original git.)
      - In the folder Runtime, script Importer.cs, add in the head `using System.Globalization;`
      - In the same script Importer.cs, function StringToVec3(string str) add the arguments `NumberStyles.Float` and `CultureInfo.InvariantCulture` for x,y and z. It should look like this:
```
float.TryParse(array[0], NumberStyles.Float, CultureInfo.InvariantCulture, out result.x);
float.TryParse(array[1], NumberStyles.Float, CultureInfo.InvariantCulture, out result.y);
float.TryParse(array[2], NumberStyles.Float, CultureInfo.InvariantCulture, out result.z);
```

3. **Download Required Third-Party Assets**:
    - [SteamVR Plugin](https://assetstore.unity.com/packages/tools/integration/steamvr-plugin-32647)
    - [Runtime OBJ Importer](https://assetstore.unity.com/packages/tools/modeling/runtime-obj-importer-49547)
    - Import these assets into your Unity project.

4. **Download Optional Third-Party Assets**:
    - [Door Free Pack Aferar](https://assetstore.unity.com/packages/3d/props/interior/door-free-pack-aferar-148411)
    - [Simple Garage](https://assetstore.unity.com/packages/3d/props/interior/simple-garage-197251)
    - [VIS - PBR Grass Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/vis-pbr-grass-textures-198071)
    - [Skybox Series Free](https://assetstore.unity.com/packages/2d/textures-materials/sky/skybox-series-free-103633)
    - Import these assets into your Unity project.

5. **Include the ISH3DE Unity Package**:
    - Download it from this repository.
    - Open your Unity project and go to `Assets > Import Package > Custom Package...`.
    - Select and import it.

6. **Prepare upper torso data from MedShapeNet**
    - all shapes with *s0011* from [their official Website](https://medshapenet-ikim.streamlit.app/)
    - in your Unity project, navigate to `Assets > ISH3DE > Scenes`, open the scenes, go to the gameObject `DataContainerUpperTorso`, in the inspector: provide the correct datapath of the data

7. **Further Settings**
    - Go to `Edit > Project Settings > XR Plug-in Management > OpenVR` and change the `Stereo Rendering Mode` to Multi Pass

8. **Without the Optional Third-Party Assets**
    - remove in the scenes the gameObjects `Room` and `Outside_stuff`

## Usage Instructions

1. to ensure that the HTC Vive Trackers are assigned to the correct haptic gloves, ensure the following order when turning for starting the HTC Vive devices:
    1. ensure that SteamVR/ViveConsole is not turned on
    2. connect all cables between the HTC Vive Pro 2 and the computer, plug in the base stations.
    3. turn on the HTC Vive Pro 2 by turning on the Linkbox, SteamVR should now start automatically
    4. when base stations are shown as detected by SteamVR, turn on the controller
    5. turn on the HTC Vive tracker attached the left haptic glove
    6. turn on the HTC Vive tracker attached the right haptic glove

2. do a SteamVR Room-Setup

3. if you want to use the haptic gloves, turn them on, open the SenseCom software and calibrate the haptic gloves

4. choose the correct scene in Unity dependent on if you want to use the haptic gloves or the controller in `Assets > ISH3DE > Scenes` or your own one

5. press *start* and wait, the loading takes some time as all stl shapes need to be loaded and transformed into the correct data format

6. when starting the project for the first time, Unity will ask you to generate actions for SteamVR, press the button yes, then press the button save and generate

## License

- ISH3DE: MIT License
- Third-party assets and packages: Refer to their respective licenses.

