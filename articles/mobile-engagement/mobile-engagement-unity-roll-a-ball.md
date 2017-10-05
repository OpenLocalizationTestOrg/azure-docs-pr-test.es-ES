---
title: juego de Rodar la bola de Unity
description: "Pasos para crear el juego clásico de Rodar una bola, que es un requisito previo de todos los tutoriales de Unity para Mobile Engagement."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6392d1f780b1bc2348fee5947550b05e86ea4de2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="f9dd3-103"><a id="unity-roll-a-ball"></a>Creación de un juego de Rodar la bola de Unity</span><span class="sxs-lookup"><span data-stu-id="f9dd3-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="f9dd3-104">Este tutorial le lleva por los pasos principales de un tutorial ligeramente modificado del [juego de Rodar la bola de Unity](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="f9dd3-105">Este juego de ejemplo consta de un objeto esférico, el "jugador", que controla el usuario de la aplicación, y el objetivo del juego consiste en ir recopilando los objetos recopilables al chocar con ellos.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span></span> <span data-ttu-id="f9dd3-106">Se supone que está familiarizado con los aspectos básicos del entorno del Editor de Unity.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="f9dd3-107">Si se tropieza con algún problema, consulte el tutorial completo.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-107">If you run into any issues then you should refer to the full tutorial.</span></span> 

### <a name="setting-up-the-game"></a><span data-ttu-id="f9dd3-108">Configuración del juego</span><span class="sxs-lookup"><span data-stu-id="f9dd3-108">Setting up the game</span></span>
<span data-ttu-id="f9dd3-109">Los pasos siguientes son del [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="f9dd3-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="f9dd3-110">Abra el **Editor de Unity** y haga clic en **New** (Nuevo).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="f9dd3-111">Proporcione datos para **Project name** (Nombre del proyecto) y  & **Location** (Ubicación) seleccione **3D** y haga clic en **Create project** (Crear proyecto).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="f9dd3-112">Guarde la escena predeterminada que acaba de crear como parte del nuevo proyecto con el nombre **MiniGame** (MiniJuego) en una nueva carpeta **\_Scenes** (Escenas) en la carpeta **Assets** (Activos):</span><span class="sxs-lookup"><span data-stu-id="f9dd3-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="f9dd3-113">En **3D Object (Objeto 3D) -> Plane (Plano)**, cree un objeto 3D plano como campo de juego y llame a este objeto plano **Ground** (Terreno).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="f9dd3-114">Restablezca el componente de transformación de este objeto **Ground** (Terreno) de modo que esté en el origen.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="f9dd3-115">Desactive **Show Grid** (Mostrar cuadrícula) en **Gizmos menu** (Menú Gizmos) para el objeto **Ground** (Terreno).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="f9dd3-116">Actualice el componente **Scale** (Escala) del objeto **Ground** (Terreno) a [X = 2,Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="f9dd3-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="f9dd3-117">En **3D Object (Objeto 3D) -> Sphere (Esfera)**, agregue un nuevo objeto 3D esférico y llame a este objeto esférico **Player** (Jugador).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="f9dd3-118">Seleccione el objeto **Player** (Jugador) y haga clic en **Reset Transform** (Restablecer transformación) igual que hizo con el objeto plano.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span></span> 
10. <span data-ttu-id="f9dd3-119">Actualice el componente **Transform (Transformación) -> Position (Posición) -> Y Coordinate (Coordenada Y)** para Player Y (Jugador Y) a 0.5.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="f9dd3-120">Cree una nueva carpeta llamada **Materials** (Materiales) en el proyecto donde vamos a crear el material para colorear el jugador.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span></span> 
12. <span data-ttu-id="f9dd3-121">Cree un nuevo **material** llamado **Background** (Fondo) en esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="f9dd3-122">Actualice el color del material actualizando su propiedad **Albedo** .</span><span class="sxs-lookup"><span data-stu-id="f9dd3-122">Update the color of the material by updating the **Albedo** property of it.</span></span> <span data-ttu-id="f9dd3-123">Puede seleccionar los valores RGB de [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="f9dd3-123">You can select the RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="f9dd3-124">Arrastre este material a la vista de escena para aplicar el color al objeto **Ground** (Terreno).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-124">Drag this material into the scene view to apply color to the **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="f9dd3-125">Finalmente, actualice los valores de **Transform (Transformación)-> Rotation (Rotación) -> Y** a 60 en el objeto Directional Light (Luz direccional) para definir la claridad.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-the-player"></a><span data-ttu-id="f9dd3-126">Movimiento del jugador</span><span class="sxs-lookup"><span data-stu-id="f9dd3-126">Moving the player</span></span>
<span data-ttu-id="f9dd3-127">Los pasos siguientes son del [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="f9dd3-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="f9dd3-128">Agregue un componente **RigidBody** al objeto **Player** (Jugador).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-128">Add a **RigidBody** component to the **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="f9dd3-129">Cree una carpeta nueva llamada **Scripts** en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-129">Create a new folder called **Scripts** in the Project.</span></span> 
3. <span data-ttu-id="f9dd3-130">Haga clic en **Add Component (Agregar componente)-> New Script (Nuevo script) -> C# Script (Script de C#)**.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="f9dd3-131">Asígnele el nombre **PlayerController** y haga clic en **Create and Add** (Crear y agregar).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="f9dd3-132">De esta forma se creará y adjuntará un script al objeto Player (Jugador).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-132">This will create and attach a script to the Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="f9dd3-133">Mueva este script a la carpeta **Scripts** del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-133">Move this script under the **Scripts** folder in the project.</span></span> 
5. <span data-ttu-id="f9dd3-134">Abra el script para editarlo en su editor de scripts preferido, actualice el código del script con el siguiente código y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="f9dd3-135">Tenga en cuenta que el script anterior usa una propiedad **Speed** .</span><span class="sxs-lookup"><span data-stu-id="f9dd3-135">Note that the script above uses a **Speed** property.</span></span> <span data-ttu-id="f9dd3-136">En el Editor de Unity, actualice esta propiedad a 10.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-136">In the Unity editor, update the speed property to 10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="f9dd3-137">Presione **Play** (Reproducir) en el Editor de Unity.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-137">Hit **Play** in the Unity Editor.</span></span> <span data-ttu-id="f9dd3-138">Ahora la bola debe poder controlarse mediante el teclado y debe girar y moverse.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span></span> 

### <a name="moving-the-camera"></a><span data-ttu-id="f9dd3-139">Movimiento de la cámara</span><span class="sxs-lookup"><span data-stu-id="f9dd3-139">Moving the camera</span></span>
<span data-ttu-id="f9dd3-140">Los pasos siguientes son del [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) y en ellos se asociará el objeto **Main Camera** (Cámara principal) al objeto **Player** (Jugador).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span></span> 

1. <span data-ttu-id="f9dd3-141">Actualice **Transform.Position** a X = 0, Y = 10.5, Z=-10.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="f9dd3-142">Actualice **Transform.Rotation** a X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="f9dd3-143">Agregue un nuevo script llamado **CameraController** a **MainCamera** y muévalo a la carpeta Scripts.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="f9dd3-144">Abra el script para editarlo y agréguele el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="f9dd3-144">Open up the script for editing and add the following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="f9dd3-145">En el entorno de Unity, arrastre la variable Player a la ranura Player del objeto Main Camera (Cámara principal) de modo que los dos queden asociados.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="f9dd3-146">Ahora, si hace clic en Play (Reproducir) en el Editor de Unity y gira el objeto Player Ball (Bola jugador), verá cómo la cámara sigue su movimiento.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span></span>  

### <a name="setting-up-the-play-area"></a><span data-ttu-id="f9dd3-147">Configuración del área de juego</span><span class="sxs-lookup"><span data-stu-id="f9dd3-147">Setting up the Play area</span></span>
<span data-ttu-id="f9dd3-148">Los pasos siguientes son del [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="f9dd3-149">Vamos a crear las paredes que rodean el terreno para que el objeto Player Ball (Bola jugador) no se salga del área de juego en su movimiento.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span></span> 

1. <span data-ttu-id="f9dd3-150">Haga clic en **Create (Crear) -> Create Empty (Crear vacío) -> Game Object (Objeto de juego)** y asigne el nombre **Walls** (Paredes).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="f9dd3-151">En este objeto Walls (Paredes), cree un nuevo objeto 3D cúbico en **3D Object (Objeto 3D) -> Cube (Cubo)** y llámelo "West Wall" (Pared oeste).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="f9dd3-152">Actualice los datos de **Transform (Transformación) -> Position (Posición)** y **Transform (Transformación) -> Scale (Escala)** de este objeto.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="f9dd3-153">Duplique el objeto West Wall (Pared oeste) para crear un objeto **East Wall** (Pared este) con la posición y la escala de transformación actualizadas.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="f9dd3-154">Duplique el objeto East Wall (Pared este) para crear un objeto **North Wall** (Pared norte) con la posición y la escala de transformación actualizadas.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="f9dd3-155">Duplique el objeto North Wall (Pared norte) y cree un objeto **South Wall** (Pared sur) con la posición y la escala de transformación actualizadas.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="f9dd3-156">Creación de objetos recopilables</span><span class="sxs-lookup"><span data-stu-id="f9dd3-156">Creating Collectible objects</span></span>
<span data-ttu-id="f9dd3-157">Los pasos siguientes son del [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="f9dd3-158">Crearemos algunos objetos atractivos que constituirán el conjunto de objetos recopilables que el objeto Player Ball (Bola jugador) debe recopilar chocando con ellos.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="f9dd3-159">Cree un nuevo **objeto cubo 3D** y llámelo Pickup (Recogida).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="f9dd3-160">Ajuste los valores de **Transform (Transformación) -> Rotation (Rotación)** &  y **Transform (Transformación) -> Scale (Escala)** del objeto Pickup (Recogida).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="f9dd3-161">Cree y asocie un **nuevo script de C#** denominado **Rotator** al objeto Pickup (Recogida).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span></span> <span data-ttu-id="f9dd3-162">Asegúrese de colocar el script en la carpeta Scripts.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-162">Make sure to put the script under the Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="f9dd3-163">Abra este script para editarlo y actualizarlo a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9dd3-163">Open this script for editing and update it to be the following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="f9dd3-164">Ahora, presione el modo Play (Reproducir) del Editor de Unity y el objeto Pickup (Recogida) se mostrará girando sobre su eje.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="f9dd3-165">Cree una nueva carpeta llamada **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="f9dd3-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="f9dd3-166">Arrastre el objeto **Pickup** (Recogida) y colóquelo en la carpeta Prefabs (Prefabricados).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-166">Drag the **Pickup** object and put it in the Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="f9dd3-167">Cree un nuevo **objeto de juego vacío** llamado **Pickups** (Recogidas).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="f9dd3-168">Restablezca su posición al origen y arrastre el objeto Pickup (Recogida) a este objeto de juego.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-168">Reset its position to origin and then drag the Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="f9dd3-169">Duplique el objeto **Pickup** (Recogida) y distribúyalo por el objeto **Ground** (Terreno) alrededor del objeto **Player** (Jugador) actualizando los valores X y Z de **Transform.Position** de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="f9dd3-170">Cree un **nuevo material** llamado **Pickup** (Recogida) y actualícelo para que sea de color rojo; para ello, actualice la **propiedad Albedo** de manera parecida a como lo hicimos para actualizar el objeto Ground (Terreno).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="f9dd3-171">Aplique el material a los 4 objetos de recogida.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-171">Apply the material to all the 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-the-pickup-objects"></a><span data-ttu-id="f9dd3-172">Recopilación de objetos de recogida</span><span class="sxs-lookup"><span data-stu-id="f9dd3-172">Collecting the Pickup objects</span></span>
<span data-ttu-id="f9dd3-173">Los pasos siguientes son del [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="f9dd3-174">Actualizaremos el objeto Player (Jugador) para que pueda recopilar los objetos Pickup (Recogida) al chocar con ellos.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="f9dd3-175">Abra el script **Playercontroller** asociado al objeto Player (Jugador) para editarlo y actualizarlo a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9dd3-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="f9dd3-176">Cree una nueva **etiqueta** llamada **Pick up** (Recogida) (debe coincidir con lo que está en el script).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="f9dd3-177">Aplique esta **etiqueta** al objeto Prefab Pickup (Recogida prefabricados).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-177">Apply this **Tag** to the Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="f9dd3-178">Active la casilla **IsTrigger** para el objeto Prefab (Prefabricado).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-178">Enable **IsTrigger** checkbox for the Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="f9dd3-179">Agregue un componente Rigid Body al objeto Pickup Prefab (Recogida prefabricados).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-179">Add a Rigid body to Pickup Prefab object.</span></span> <span data-ttu-id="f9dd3-180">Para optimizar el rendimiento, actualizaremos el colisionador estático que hemos usado a colisionador dinámico.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="f9dd3-181">Finalmente, marque la propiedad **IsKinematic** del objeto Prefab (Prefabricado).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-181">Finally check the **IsKinematic** property for the prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="f9dd3-182">Presione **Play** (Reproducir) en el Editor de Unity y podrá jugar a este juego de **Rodar la bola** moviendo el objeto Player (Jugador) con las teclas del teclado para indicar la dirección.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-the-game-for-mobile-play"></a><span data-ttu-id="f9dd3-183">Actualización del juego para dispositivos móviles</span><span class="sxs-lookup"><span data-stu-id="f9dd3-183">Updating the game for mobile play</span></span>
<span data-ttu-id="f9dd3-184">En las secciones anteriores hemos concluido el tutorial básico de Unity.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-184">The sections above concluded the basic tutorial from Unity.</span></span> <span data-ttu-id="f9dd3-185">Ahora modificaremos el juego para que pueda usarse en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-185">Now we will modify the game to make it mobile device friendly.</span></span> <span data-ttu-id="f9dd3-186">Tenga en cuenta que hasta ahora hemos usado la entrada del teclado para probar el juego.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-186">Note that we used keyboard input for the game so far for testing.</span></span> <span data-ttu-id="f9dd3-187">Ahora vamos a cambiar eso de modo que podamos controlar el jugador con el movimiento del teléfono, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="f9dd3-187">Now we will modify it so that we can control the player by using the motion of the phone i.e.</span></span> <span data-ttu-id="f9dd3-188">usando el acelerómetro como entrada.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-188">using Accelerometer as the input.</span></span> 

<span data-ttu-id="f9dd3-189">Abra el script **PlayerController** para editarlo y actualice el método **FixedUpdate** para usar el movimiento del acelerómetro para mover el objeto Player (Jugador).</span><span class="sxs-lookup"><span data-stu-id="f9dd3-189">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="f9dd3-190">Con este tutorial concluye la creación de un juego básico con Unity, que puede implementar para jugar en el dispositivo de su elección.</span><span class="sxs-lookup"><span data-stu-id="f9dd3-190">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













