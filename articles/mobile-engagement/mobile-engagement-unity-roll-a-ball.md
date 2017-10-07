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
# <a id="unity-roll-a-ball"></a>Creación de un juego de Rodar la bola de Unity
Este tutorial le guía a través de los pasos principales de Hola para ligeramente modificada [Unity poner un tutorial de bola](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). Este juego de ejemplo consta de un objeto esférica 'jugador' que está controlado por el usuario de la aplicación de Hola y objetivo de Hola de juego hello es too'collect' recopilables objetos por objeto de Reproductor Hola colisión con estos objetos recopilables. Se supone que está familiarizado con los aspectos básicos del entorno del Editor de Unity. Si surge algún problema, a continuación, se debe hacer referencia tutorial completo toohello. 

### <a name="setting-up-hello-game"></a>Configuración de juego Hola
Hola pasos son de hello [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Abra el **Editor de Unity** y haga clic en **New** (Nuevo). 
   
    ![][51] 
2. Proporcione datos para **Project name** (Nombre del proyecto) y  & **Location** (Ubicación) seleccione **3D** y haga clic en **Create project** (Crear proyecto).
   
    ![][52]
3. Guardar Hola predeterminado escena acaba de crear como parte del nuevo proyecto de hello al igual que con el nombre de hello **MiniGame** dentro de un nuevo  **\_plano** carpeta bajo **activos** carpeta:
   
    ![][53]
4. Crear un **objeto 3D -> plano** como "reproduciendo" Hola, campo y cambiar el nombre de este objeto de plano como **terreno**
   
    ![][1]
5. Componente de transformación de Hola de restablecimiento para esta **terreno** para que resulte en hello origen del objeto. 
   
    ![][3]
6. Desactive la opción **Mostrar cuadrícula** de **menú chismes** para hello **terreno** objeto.
   
    ![][4]
7. Hola de actualización **escala** componente para hello **terreno** objeto toobe [X = 2, Y = 1, Z = 2]. 
   
    ![][5]
8. Agregue un nuevo **objeto 3D -> esfera** toohello proyecto y cambie el nombre del objeto como esta esfera **Reproductor**. 
   
    ![][6]
9. Seleccione hello **Reproductor** objeto y haga clic en **Restablecer transformación** objeto de plano toohello similar. 
10. Actualización **transformación -> posición -> coordenada** componente para hello Y Reproductor como 0,5.  
    
    ![][7]
11. Cree una carpeta nueva denominada **materiales** en proyecto de Hola donde se creará el Reproductor de hello toocolor material Hola. 
12. Cree un nuevo **material** llamado **Background** (Fondo) en esta carpeta. 
    
    ![][8]
13. Actualizar el color de Hola de material de hello actualizando Hola **Albedo** propiedad del mismo. Puede seleccionar los valores RGB Hola de [0,32,64]. 
    
    ![][9]
14. Arrastre este material Hola escena vista tooapply color toohello **terreno** objeto. 
    
    ![][10]
15. Por último, actualizar hello **transformación -> rotación -> Y** too60 en objeto de luz direccional de Hola para mayor claridad. 
    
    ![][12]

### <a name="moving-hello-player"></a>Reproductor de hello móvil
Hola pasos son de hello [tutorial de Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Agregar un **RigidBody** componente toohello **Reproductor** objeto. 
   
    ![][13]
2. Cree una carpeta nueva denominada **Scripts** Hola proyecto. 
3. Haga clic en **Add Component (Agregar componente)-> New Script (Nuevo script) -> C# Script (Script de C#)**. Asígnele el nombre **PlayerController** y haga clic en **Create and Add** (Crear y agregar). Esto creará y adjuntar un objeto de secuencia de comandos toohello Reproductor.  
   
    ![][14]
4. Mueva este script en hello **Scripts** carpeta proyecto Hola. 
5. Abrir el script de Hola para su edición en su editor favorito de la secuencia de comandos, actualice el código de script de Hola con el siguiente código de hello y guárdelo. 
   
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
6. Tenga en cuenta esa secuencia de comandos de hello anterior se usa un **velocidad** propiedad. En el editor de Unity hello, actualizar Hola velocidad propiedad too10.  
   
    ![][15]
7. Aciertos **reproducir** Hola Editor de Unity. Ahora debe ser la bola de hello toocontrol capaz de usar teclado hello y debe girar y moverse. 

### <a name="moving-hello-camera"></a>Cámara de hello móvil
Hola pasos son de hello [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) y se asociará hello **Main cámara** toohello **Reproductor** objeto. 

1. Hola de actualización **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.  
2. Hola de actualización **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Agregar un script nuevo denominado **CameraController** toohello **MainCamera** y muévala a la carpeta de Scripts de Hola. 
   
    ![][17]
4. Abra una secuencia de comandos de Hola para su edición y agregue Hola siguiente código en él:
   
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
5. En el entorno de Unity: arrastre variable del Reproductor de hello en la ranura de Reproductor de hello para el objeto de cámara principal de Hola para que hello dos están asociadas con otro. 
   
    ![][18]
6. Ahora si presiona la tecla Play en editor de Unity de Hola y el objeto de Reproductor bola Hola girar, a continuación, verá Hola cámara después en movimiento Hola.  

### <a name="setting-up-hello-play-area"></a>Configuración de área de reproducción de Hola
Hola pasos son de hello [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Crearemos paredes de Hola que rodean Hola terreno para que hello objeto bola del Reproductor no entrega área de reproducción de hello en su movimiento. 

1. Haga clic en **Create (Crear) -> Create Empty (Crear vacío) -> Game Object (Objeto de juego)** y asigne el nombre **Walls** (Paredes).
   
    ![][19]
2. En este objeto Walls (Paredes), cree un nuevo objeto 3D cúbico en **3D Object (Objeto 3D) -> Cube (Cubo)** y llámelo "West Wall" (Pared oeste). 
   
    ![][20]
3. Hola de actualización **transformación -> posición** y **transformación -> escala** para este objeto de pared oeste. 
   
    ![][21]
4. Duplicar Hola oeste pared toocreate una **pared este** con hello actualizado transformar la posición y la escala. 
   
    ![][22]
5. Duplicar Hola este pared toocreate una **pared Norte** con hello actualizado transformar la posición y ajustar la escala. 
   
    ![][23]
6. Duplicar la pared de hello Norte y crear un **pared sur** con hello actualizado transformar la posición y ajustar la escala. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>Creación de objetos recopilables
Hola pasos son de hello [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Crearemos algunas atractivos buscar objetos que conformarán conjunto de Hola de objetos recopilables qué objeto de Reproductor bola Hola necesita too'collect' por entren con ellos. 

1. Cree un nuevo **objeto cubo 3D** y llámelo Pickup (Recogida). 
2. Ajustar hello **transformación -> rotación** & **transformación -> escala** del objeto de recogida de Hola. 
   
    ![][25]
3. Crear y adjuntar un **nuevo Script de C#** llama **rotación** toohello recogida objeto. Asegúrese de script de Hola tooput seguro en la carpeta de Scripts de Hola. 
   
    ![][26]
4. Abra este script para su edición y actualícelo hello toobe siguientes: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Ahora se rotación de modo de reproducción de posicionamiento hello en hello Editor de Unity y el programa de objeto recogida en el eje.
6. Cree una nueva carpeta llamada **Prefabs** 
   
    ![][27]
7. Hola arrastre **recogida** objeto y colóquelo en la carpeta de Prefabs Hola.
   
    ![][28]
8. Cree un nuevo **objeto de juego vacío** llamado **Pickups** (Recogidas). Restablecer su tooorigin de posición y, a continuación, arrastre el objeto de recogida de hello bajo este objeto de juego.  
   
    ![][29]
9. Hola duplicado **recogida** objeto y repartidas en hello **terreno** objeto alrededor de hello **Reproductor** objeto actualizando hello **del Transform.Position X & Z**  valores correctamente. 
   
    ![][30]
10. Crear un **nuevo material** llama **recogida** y actualizarla toobe rojo en color actualizando hello **propiedad Albedo** toowhat similar se para actualizar Hola tierra del objeto. 
    
    ![][31]
11. Aplicar hello tooall material Hola 4 recogida objetos.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>Recopilación de objetos de recogida de Hola
Hola pasos son de hello [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Actualizaremos Hola Reproductor para que sea capaz de too'collect' hello objetos recogidos por entren con ellos. 

1. Abra hello **PlayerController** generar un script adjunto toohello Reproductor objeto para su edición y actualizarla toohello siguientes:  
   
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
2. Crear un nuevo **etiqueta** llama **elegir una** (debe coincidir con lo que aparece en el script de Hola)  
   
    ![][33]
   
    ![][34]
3. Aplicar este **etiqueta** objeto de recogida Prefab toohello. 
   
    ![][35]
4. Habilitar **IsTrigger** casilla de verificación hello Prefab objeto.
   
    ![][36]
5. Agregar un objeto de cuerpo rígida tooPickup Prefab. Para optimizar el rendimiento actualizamos collider estático Hola que hemos usado tooa dinámico collider. 
   
    ![][37]
6. Por último, comprobar hello **IsKinematic** propiedad del objeto prefab Hola. 
   
    ![][38]
7. Aciertos **reproducir** en el editor de Unity hello y será capaz de tooplay este **poner una bola** juego moviendo Hola objeto Reproductor utilizando las teclas del teclado para la entrada de dirección. 

### <a name="updating-hello-game-for-mobile-play"></a>Actualizar Hola juego para móvil play
secciones de Hello anteriormente tutorial básico de hello terminada desde Unity. Ahora vamos a modificar Hola toomake juego lo descriptivo de dispositivos móviles. Tenga en cuenta que utilizamos entrada de teclado para hello juego hasta ahora para realizar pruebas. Ahora vamos a modificar, por lo que podemos controlar Reproductor hello mediante el uso de movimiento de Hola de hello teléfono es decir, mediante acelerómetro como entrada de Hola. 

Abra hello **PlayerController** secuencia de comandos para editar y actualizar hello **FixedUpdate** movimiento de hello toouse de método del objeto de Reproductor de hello acelerómetro toomove Hola. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Este tutorial finaliza la creación de un juego básica con Unity y se puede implementar en un dispositivo de su juego de elección tooplay Hola. 

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













