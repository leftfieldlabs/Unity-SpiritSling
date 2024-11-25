# Spirit Sling Tabletop
![Banner](./Documentation/Images/SpiritSling_Marketing_SmallLandscape.png)

Spirit Sling is an immersive tabletop game that demonstrates how to build a mixed reality multiplayer experience using enhanced Meta Avatars and capabilities like Platform SDK and Interaction SDK. Up to four players use their wit and strategically placed slingshots to maneuver mystical creatures across a dynamic gameboard.

# Before you get started

Before you dive in, ensure you’ve downloaded and installed the necessary packages to run Spirit Sling on Unity. 

- [Mixed Reality Utility Kit](https://developers.meta.com/horizon/documentation/unity/unity-mr-utility-kit-overview/) (MRUK) v69 or later: This set of utilities includes scene queries, graphical helpers, and development tools that make it easier to perform common operations when building spatially-aware apps with Scene API.
- [Meta XR Core SDK](https://assetstore.unity.com/packages/tools/integration/meta-xr-core-sdk-269169) v69 or later: This package includes core features for mixed reality development such as Passthrough, Anchors, and Scene to help you create engaging and immersive experiences.
- [Meta XR Interaction SDK](https://assetstore.unity.com/packages/tools/integration/meta-xr-interaction-sdk-265014) v69 or later: This package contains the unique Interaction SDK components used for controller and hand interactions and body pose detection.
- [Meta Avatars SDK](https://assetstore.unity.com/packages/tools/integration/meta-avatars-sdk-271958) v29.7.0 or later: This package enables you to enhance presence and immersion by giving your app’s users a unique sense of self with advanced body tracking and modularized full-bodied torsos.
- [Meta XR Platform SDK](https://assetstore.unity.com/packages/tools/integration/meta-xr-platform-sdk-262366): This package enables you to create social immersive experiences that support matchmaking, in-app purchases, downloadable content (DLC), cloud storage, and more.
- [Photon Fusion](https://www.photonengine.com/fusion#): Seamlessly support multiplayer modes by implementing this networking solution to handle and route networking traffic in shared user experiences.

# Learn 
Explore the Meta Horizon OS capabilities powering rich, shared mixed reality experiences in Spirit Sling. 

- [Mixed Reality Utility Kit](https://developers.meta.com/horizon/documentation/unity/unity-mr-utility-kit-overview/) (MRUK): Learn how MRUK can be used to ensure the virtual gameboard is placed on an ideal surface and supports seamless and accessible gameplay.
- [Platform SDK](https://developers.meta.com/horizon/downloads/package/oculus-platform-sdk/): Learn how you can use Platform SDK’s social features like Party Chat and User Reporting to build an engaging and safe multiplayer experience.
- [Interaction SDK](https://developers.meta.com/horizon/documentation/unity/unity-isdk-interaction-sdk-overview/): Discover how to enable hand interactions with virtual objects to enhance traditional tabletop gameplay mechanics and increase feelings of presence.
- [Meta Avatars SDK](https://developers.meta.com/horizon/documentation/unity/meta-avatars-overview/): See first-hand how Meta Avatars enhance social experiences and cultivate deeper connections through natural, animated facial expressions and realistic body poses.
- [Scene](https://developers.meta.com/horizon/documentation/unity/unity-scene-overview/): Index and query an up-to-date representation of the physical world. Scene enables Spirit Sling to access data from real-world objects so the game board can be accessible to players.

# Mechanics and Features
Discover some of the mechanics, features, and techniques used to deliver this unique and engaging multiplayer experience. For more information, visit the [documentation](https://developers.meta.com/horizon/documentation/unity/spirit-sling/).

- [Contextual game board placement](https://developers.meta.com/horizon/documentation/unity/spirit-sling/#contextual-board-placement-mixed-reality-utility-kit--other-tips): Using Scene API and MRUK, Spirit Sling accesses real-world object data to ensure that the game board is immediately accessible to users’ hands and maintains visibility above real-world objects.
- [Creating and joining a multiplayer session](https://developers.meta.com/horizon/documentation/unity/spirit-sling/#creating-a-multiplayer-session): Spirit Sling supports players joining public or private multiplayer sessions. After the Platform SDK is initialized, the app creates a public or private multiplayer room by calling Fusion.NetworkRunner.StartGame(...) or GroupPresence.Set(...), respectively. A public session is joined by first subscribing to the NetworkEvents.OnSessionListUpdate event, then NetworkRunner.JoinSessionLobby(...)and finally finding and joining the first non-full public room calling NetworkRunner.StartGame(...). For a private lobby, the app reads ApplicationLifecycle.GetLaunchDetails() to accept the invite. The app also subscribes to the ApplicationLifecycle.SetLaunchIntentChangedNotificationCallback() callback to listen for the launch intent changes.
- [Hand tracking integration](https://developers.meta.com/horizon/documentation/unity/spirit-sling/#intractable-virtual-objects-using-isdk-and-physics-to-enhance-gameplay): Spirit Sling supports hand tracking as a primary form of input when users interact with the gameboard. Hand tracking and Grab interactions can be integrated using Interaction SDK through the Building Blocks tool.
- [Using Interaction SDK to control gameplay](https://developers.meta.com/horizon/documentation/unity/spirit-sling/#using-isdk-to-control-gameplay-elements): Users can control and manipulate gameplay elements through the app’s ability to detect grab gestures using the Grabbable,HandGrabInteractable, and GrabInteractable components.
- [Game board adjustment with hand tracking](https://developers.meta.com/horizon/documentation/unity/spirit-sling/#manual-board-adjustment-with-hand-tracking): To support an adaptable and comfortable user experience, the game enables users to re-adjust the board after initial placement using the Grabbable component from ISDK and custom One/TwoGrabGameVolumeTransformer components.
- [Adding hand interactions to interface buttons](https://developers.meta.com/horizon/documentation/unity/spirit-sling/#adding-hand-interaction-to-interface-buttons): Users can leverage the poke interaction to navigate the game’s user interface. Poke interaction support can be enabled by adding the Poke Interaction building block, creating a SpiritSlingButton script and attaching it to a game object that includes the PokeInteractable component.  

# How to run the project in Unity
1. [Configure the project](./Documentation/ProjectConfiguration.md) with Meta Quest and Photon
2. Make sure you're using 2022.3.30.
3. Make sure you're using one of these devices: Meta Quest 3S, Meta Quest 3, Meta Quest Pro.
4. Locate the 'Assets/GameSettings.asset' file and populate all the empty fields with your own data.  
4.1. 'Application Identifier' is the unique string that identifies your app on Meta Quest Store.  
4.2. 'Meta Quest App ID' is the ID of your app on Meta Quest Store.  
4.3. Optional: populate Android Keystore name and password. Make sure not to store the 'Assets/GameSettings.asset' file in VCS in this case.  
4.4. 'Photon App Id Fusion / Voice': unique ids obtained in step 1 in the 'Photon Configuration' section.
![Game Settings](./Documentation/Images/GameSettings.png)

# Project Structure
The project is organically structured to distinguish the main components of the MR experience's logic. Main Spirit Sling components:
- **ConnectionManager** handles the Photon Fusion connection workflows for single and multiplayer sessions. The PhotonConnector logic showcases how a shared multiplayer session is handled via Photon Fusion, how the creation of shared rooms and lobbies work, and how the connection states can be handled accordingly.
- **GameVolumeSpawner** handles logic for placing the game board into physical environment. It also ensures that the game board is accessible by hands so the user can readjust the initial placement for a more comfortable experience.
- **TabletopGameStateMachine** controls the flow of the game between different gameplay states.
- Please visit the [Meta Horizon Documentation](https://developers.meta.com/horizon/documentation/unity/spirit-sling/#intractable-virtual-objects-using-isdk-and-physics-to-enhance-gameplay) page for more details on how the game uses Mixed Reality Utility Kit (MRUK), Platform SDK and Meta Interaction SDK (ISDK).

# Dependencies
This project makes use of the following plugins and software:
- [Mixed Reality Utility Kit v69](https://developers.meta.com/horizon/documentation/unity/unity-mr-utility-kit-overview/)
- [Meta XR Core SDK v69](https://developers.meta.com/horizon/downloads/package/meta-xr-core-sdk)
- [Meta Interaction SDK v69](https://developers.meta.com/horizon/documentation/unity/unity-isdk-interaction-sdk-overview/)
- [Meta Avatars SDK v29.7.0](https://developers.meta.com/horizon/documentation/unity/meta-avatars-overview/)

The majority of Spirit Sling is licensed under [MIT LICENSE](./LICENSE), however files from [Text Mesh Pro](http://www.unity3d.com/legal/licenses/Unity_Companion_License), and [Photon SDK](./Assets/Photon/LICENSE), are licensed under their respective licensing terms.

See the [CONTRIBUTING](./CONTRIBUTING.md) file for how to help out.

This project was built using the [Unity engine](https://unity.com/) with [Photon Fusion](https://doc.photonengine.com/fusion/current/getting-started/fusion-intro).

Test the game on [Meta Quest Store - Spirit Sling Tabletop](https://www.meta.com/en-gb/experiences/spirit-sling-tabletop/26801347429479910/).
