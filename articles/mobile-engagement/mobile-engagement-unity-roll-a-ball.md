---
title: aaaUnity poner un tutorial de bola
description: "Pasos toocreate Hola clásico Unity poner un juego con bolas que es un requisito previo para todos los tutoriales de Mobile Engagement Unity"
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
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="4cc28-103"><a id="unity-roll-a-ball"></a>Creación de un juego de Rodar la bola de Unity</span><span class="sxs-lookup"><span data-stu-id="4cc28-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="4cc28-104">Este tutorial le guía a través de los pasos principales de Hola para ligeramente modificada [Unity poner un tutorial de bola](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="4cc28-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="4cc28-105">Este juego de ejemplo consta de un objeto esférica 'jugador' que está controlado por el usuario de la aplicación de Hola y objetivo de Hola de juego hello es too'collect' recopilables objetos por objeto de Reproductor Hola colisión con estos objetos recopilables.</span><span class="sxs-lookup"><span data-stu-id="4cc28-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="4cc28-106">Se supone que está familiarizado con los aspectos básicos del entorno del Editor de Unity.</span><span class="sxs-lookup"><span data-stu-id="4cc28-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="4cc28-107">Si surge algún problema, a continuación, se debe hacer referencia tutorial completo toohello.</span><span class="sxs-lookup"><span data-stu-id="4cc28-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="4cc28-108">Configuración de juego Hola</span><span class="sxs-lookup"><span data-stu-id="4cc28-108">Setting up hello game</span></span>
<span data-ttu-id="4cc28-109">Hola pasos son de hello [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="4cc28-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="4cc28-110">Abra el **Editor de Unity** y haga clic en **New** (Nuevo).</span><span class="sxs-lookup"><span data-stu-id="4cc28-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="4cc28-111">Proporcione datos para **Project name** (Nombre del proyecto) y  & **Location** (Ubicación) seleccione **3D** y haga clic en **Create project** (Crear proyecto).</span><span class="sxs-lookup"><span data-stu-id="4cc28-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="4cc28-112">Guardar Hola predeterminado escena acaba de crear como parte del nuevo proyecto de hello al igual que con el nombre de hello **MiniGame** dentro de un nuevo  **\_plano** carpeta bajo **activos** carpeta:</span><span class="sxs-lookup"><span data-stu-id="4cc28-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="4cc28-113">Crear un **objeto 3D -> plano** como "reproduciendo" Hola, campo y cambiar el nombre de este objeto de plano como **terreno**</span><span class="sxs-lookup"><span data-stu-id="4cc28-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="4cc28-114">Componente de transformación de Hola de restablecimiento para esta **terreno** para que resulte en hello origen del objeto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="4cc28-115">Desactive la opción **Mostrar cuadrícula** de **menú chismes** para hello **terreno** objeto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="4cc28-116">Hola de actualización **escala** componente para hello **terreno** objeto toobe [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="4cc28-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="4cc28-117">Agregue un nuevo **objeto 3D -> esfera** toohello proyecto y cambie el nombre del objeto como esta esfera **Reproductor**.</span><span class="sxs-lookup"><span data-stu-id="4cc28-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="4cc28-118">Seleccione hello **Reproductor** objeto y haga clic en **Restablecer transformación** objeto de plano toohello similar.</span><span class="sxs-lookup"><span data-stu-id="4cc28-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="4cc28-119">Actualización **transformación -> posición -> coordenada** componente para hello Y Reproductor como 0,5.</span><span class="sxs-lookup"><span data-stu-id="4cc28-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="4cc28-120">Cree una carpeta nueva denominada **materiales** en proyecto de Hola donde se creará el Reproductor de hello toocolor material Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="4cc28-121">Cree un nuevo **material** llamado **Background** (Fondo) en esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="4cc28-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="4cc28-122">Actualizar el color de Hola de material de hello actualizando Hola **Albedo** propiedad del mismo.</span><span class="sxs-lookup"><span data-stu-id="4cc28-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="4cc28-123">Puede seleccionar los valores RGB Hola de [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="4cc28-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="4cc28-124">Arrastre este material Hola escena vista tooapply color toohello **terreno** objeto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="4cc28-125">Por último, actualizar hello **transformación -> rotación -> Y** too60 en objeto de luz direccional de Hola para mayor claridad.</span><span class="sxs-lookup"><span data-stu-id="4cc28-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="4cc28-126">Reproductor de hello móvil</span><span class="sxs-lookup"><span data-stu-id="4cc28-126">Moving hello player</span></span>
<span data-ttu-id="4cc28-127">Hola pasos son de hello [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="4cc28-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="4cc28-128">Agregar un **RigidBody** componente toohello **Reproductor** objeto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="4cc28-129">Cree una carpeta nueva denominada **Scripts** Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="4cc28-130">Haga clic en **Add Component (Agregar componente)-> New Script (Nuevo script) -> C# Script (Script de C#)**.</span><span class="sxs-lookup"><span data-stu-id="4cc28-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="4cc28-131">Asígnele el nombre **PlayerController** y haga clic en **Create and Add** (Crear y agregar).</span><span class="sxs-lookup"><span data-stu-id="4cc28-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="4cc28-132">Esto creará y adjuntar un objeto de secuencia de comandos toohello Reproductor.</span><span class="sxs-lookup"><span data-stu-id="4cc28-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="4cc28-133">Mueva este script en hello **Scripts** carpeta proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="4cc28-134">Abrir el script de Hola para su edición en su editor favorito de la secuencia de comandos, actualice el código de script de Hola con el siguiente código de hello y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="4cc28-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
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
6. <span data-ttu-id="4cc28-135">Tenga en cuenta esa secuencia de comandos de hello anterior se usa un **velocidad** propiedad.</span><span class="sxs-lookup"><span data-stu-id="4cc28-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="4cc28-136">En el editor de Unity hello, actualizar Hola velocidad propiedad too10.</span><span class="sxs-lookup"><span data-stu-id="4cc28-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="4cc28-137">Aciertos **reproducir** Hola Editor de Unity.</span><span class="sxs-lookup"><span data-stu-id="4cc28-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="4cc28-138">Ahora debe ser la bola de hello toocontrol capaz de usar teclado hello y debe girar y moverse.</span><span class="sxs-lookup"><span data-stu-id="4cc28-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="4cc28-139">Cámara de hello móvil</span><span class="sxs-lookup"><span data-stu-id="4cc28-139">Moving hello camera</span></span>
<span data-ttu-id="4cc28-140">Hola pasos son de hello [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) y se asociará hello **Main cámara** toohello **Reproductor** objeto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="4cc28-141">Hola de actualización **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.</span><span class="sxs-lookup"><span data-stu-id="4cc28-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="4cc28-142">Hola de actualización **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="4cc28-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="4cc28-143">Agregar un script nuevo denominado **CameraController** toohello **MainCamera** y muévala a la carpeta de Scripts de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="4cc28-144">Abra una secuencia de comandos de Hola para su edición y agregue Hola siguiente código en él:</span><span class="sxs-lookup"><span data-stu-id="4cc28-144">Open up hello script for editing and add hello following code in it:</span></span>
   
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
5. <span data-ttu-id="4cc28-145">En el entorno de Unity: arrastre variable del Reproductor de hello en la ranura de Reproductor de hello para el objeto de cámara principal de Hola para que hello dos están asociadas con otro.</span><span class="sxs-lookup"><span data-stu-id="4cc28-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="4cc28-146">Ahora si presiona la tecla Play en editor de Unity de Hola y el objeto de Reproductor bola Hola girar, a continuación, verá Hola cámara después en movimiento Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="4cc28-147">Configuración de área de reproducción de Hola</span><span class="sxs-lookup"><span data-stu-id="4cc28-147">Setting up hello Play area</span></span>
<span data-ttu-id="4cc28-148">Hola pasos son de hello [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="4cc28-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="4cc28-149">Crearemos paredes de Hola que rodean Hola terreno para que hello objeto bola del Reproductor no entrega área de reproducción de hello en su movimiento.</span><span class="sxs-lookup"><span data-stu-id="4cc28-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="4cc28-150">Haga clic en **Create (Crear) -> Create Empty (Crear vacío) -> Game Object (Objeto de juego)** y asigne el nombre **Walls** (Paredes).</span><span class="sxs-lookup"><span data-stu-id="4cc28-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="4cc28-151">En este objeto Walls (Paredes), cree un nuevo objeto 3D cúbico en **3D Object (Objeto 3D) -> Cube (Cubo)** y llámelo "West Wall" (Pared oeste).</span><span class="sxs-lookup"><span data-stu-id="4cc28-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="4cc28-152">Hola de actualización **transformación -> posición** y **transformación -> escala** para este objeto de pared oeste.</span><span class="sxs-lookup"><span data-stu-id="4cc28-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="4cc28-153">Duplicar Hola oeste pared toocreate una **pared este** con hello actualizado transformar la posición y la escala.</span><span class="sxs-lookup"><span data-stu-id="4cc28-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="4cc28-154">Duplicar Hola este pared toocreate una **pared Norte** con hello actualizado transformar la posición y ajustar la escala.</span><span class="sxs-lookup"><span data-stu-id="4cc28-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="4cc28-155">Duplicar la pared de hello Norte y crear un **pared sur** con hello actualizado transformar la posición y ajustar la escala.</span><span class="sxs-lookup"><span data-stu-id="4cc28-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="4cc28-156">Creación de objetos recopilables</span><span class="sxs-lookup"><span data-stu-id="4cc28-156">Creating Collectible objects</span></span>
<span data-ttu-id="4cc28-157">Hola pasos son de hello [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="4cc28-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="4cc28-158">Crearemos algunas atractivos buscar objetos que conformarán conjunto de Hola de objetos recopilables qué objeto de Reproductor bola Hola necesita too'collect' por entren con ellos.</span><span class="sxs-lookup"><span data-stu-id="4cc28-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="4cc28-159">Cree un nuevo **objeto cubo 3D** y llámelo Pickup (Recogida).</span><span class="sxs-lookup"><span data-stu-id="4cc28-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="4cc28-160">Ajustar hello **transformación -> rotación** & **transformación -> escala** del objeto de recogida de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="4cc28-161">Crear y adjuntar un **nuevo Script de C#** llama **rotación** toohello recogida objeto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="4cc28-162">Asegúrese de script de Hola tooput seguro en la carpeta de Scripts de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="4cc28-163">Abra este script para su edición y actualícelo hello toobe siguientes:</span><span class="sxs-lookup"><span data-stu-id="4cc28-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="4cc28-164">Ahora se rotación de modo de reproducción de posicionamiento hello en hello Editor de Unity y el programa de objeto recogida en el eje.</span><span class="sxs-lookup"><span data-stu-id="4cc28-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="4cc28-165">Cree una nueva carpeta llamada **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="4cc28-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="4cc28-166">Hola arrastre **recogida** objeto y colóquelo en la carpeta de Prefabs Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="4cc28-167">Cree un nuevo **objeto de juego vacío** llamado **Pickups** (Recogidas).</span><span class="sxs-lookup"><span data-stu-id="4cc28-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="4cc28-168">Restablecer su tooorigin de posición y, a continuación, arrastre el objeto de recogida de hello bajo este objeto de juego.</span><span class="sxs-lookup"><span data-stu-id="4cc28-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="4cc28-169">Hola duplicado **recogida** objeto y repartidas en hello **terreno** objeto alrededor de hello **Reproductor** objeto actualizando hello **del Transform.Position X & Z**  valores correctamente.</span><span class="sxs-lookup"><span data-stu-id="4cc28-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="4cc28-170">Crear un **nuevo material** llama **recogida** y actualizarla toobe rojo en color actualizando hello **propiedad Albedo** toowhat similar se para actualizar Hola tierra del objeto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="4cc28-171">Aplicar hello tooall material Hola 4 recogida objetos.</span><span class="sxs-lookup"><span data-stu-id="4cc28-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="4cc28-172">Recopilación de objetos de recogida de Hola</span><span class="sxs-lookup"><span data-stu-id="4cc28-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="4cc28-173">Hola pasos son de hello [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="4cc28-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="4cc28-174">Actualizaremos Hola Reproductor para que sea capaz de too'collect' hello objetos recogidos por entren con ellos.</span><span class="sxs-lookup"><span data-stu-id="4cc28-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="4cc28-175">Abra hello **PlayerController** generar un script adjunto toohello Reproductor objeto para su edición y actualizarla toohello siguientes:</span><span class="sxs-lookup"><span data-stu-id="4cc28-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
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
2. <span data-ttu-id="4cc28-176">Crear un nuevo **etiqueta** llama **elegir una** (debe coincidir con lo que aparece en el script de Hola)</span><span class="sxs-lookup"><span data-stu-id="4cc28-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="4cc28-177">Aplicar este **etiqueta** objeto de recogida Prefab toohello.</span><span class="sxs-lookup"><span data-stu-id="4cc28-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="4cc28-178">Habilitar **IsTrigger** casilla de verificación hello Prefab objeto.</span><span class="sxs-lookup"><span data-stu-id="4cc28-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="4cc28-179">Agregar un objeto de cuerpo rígida tooPickup Prefab.</span><span class="sxs-lookup"><span data-stu-id="4cc28-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="4cc28-180">Para optimizar el rendimiento actualizamos collider estático Hola que hemos usado tooa dinámico collider.</span><span class="sxs-lookup"><span data-stu-id="4cc28-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="4cc28-181">Por último, comprobar hello **IsKinematic** propiedad del objeto prefab Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="4cc28-182">Aciertos **reproducir** en el editor de Unity hello y será capaz de tooplay este **poner una bola** juego moviendo Hola objeto Reproductor utilizando las teclas del teclado para la entrada de dirección.</span><span class="sxs-lookup"><span data-stu-id="4cc28-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="4cc28-183">Actualizar Hola juego para móvil play</span><span class="sxs-lookup"><span data-stu-id="4cc28-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="4cc28-184">secciones de Hello anteriormente tutorial básico de hello terminada desde Unity.</span><span class="sxs-lookup"><span data-stu-id="4cc28-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="4cc28-185">Ahora vamos a modificar Hola toomake juego lo descriptivo de dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="4cc28-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="4cc28-186">Tenga en cuenta que utilizamos entrada de teclado para hello juego hasta ahora para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="4cc28-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="4cc28-187">Ahora vamos a modificar, por lo que podemos controlar Reproductor hello mediante el uso de movimiento de Hola de hello teléfono es decir, mediante acelerómetro como entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="4cc28-188">Abra hello **PlayerController** secuencia de comandos para editar y actualizar hello **FixedUpdate** movimiento de hello toouse de método del objeto de Reproductor de hello acelerómetro toomove Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="4cc28-189">Este tutorial finaliza la creación de un juego básica con Unity y se puede implementar en un dispositivo de su juego de elección tooplay Hola.</span><span class="sxs-lookup"><span data-stu-id="4cc28-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

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













