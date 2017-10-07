---
title: aaaAzure RemoteApp - probar el uso de ancho de banda de red con algunos escenarios comunes | Documentos de Microsoft
description: "Obtenga más información sobre escenarios de uso comunes que pueden ayudarle a descubrir las necesidades de ancho de banda de la red de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp: probar el uso de ancho de banda de red con algunos escenarios comunes
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Como se explicó en [uso de ancho de banda de red de estimación Azure RemoteApp](remoteapp-bandwidth.md), Hola toofigure de manera mejor qué impacto Hola de red de Azure RemoteApp tooyour es toorun algunas pruebas de uso. Ejecutar estas pruebas para un conjunto de tiempo período y medida Hola ancho de banda necesario para cada escenario. Si tiene capacidad de hello, también puede medir Hola red pérdida y red vibración toounderstand Hola red modelos de paquetes que se creará en su entorno específico.

Al evaluar el uso de ancho de banda de hello, recuerde que uso varía entre distintos usuarios dentro de su empresa. Por ejemplo, los usuarios que escriben y leen texto suelen consumir menos ancho de banda que los usuarios que trabajan con vídeo. Para obtener mejores resultados, revise atentamente las necesidades del usuario y crear una combinación de hello los escenarios siguientes que mejor representa a los usuarios de hello en su empresa. Recuerde demasiado[factores de Hola de revisión que afectan el uso de ancho de banda y el usuario experimentan](remoteapp-bandwidthexperience.md) -que le ayudará a identificar pruebas ideal de Hola.

Leer acerca de las pruebas de hello, elegir la combinación y, a continuación, ejecutarlos. Puede usar tabla de hello siguiente toohelp seguir el rendimiento.

> [!NOTE]
> Si no puede realizar sus propias pruebas de red, o no tiene Hola tiempo toodo por lo tanto, visite nuestro [estimaciones/recomendaciones de ancho de banda de red básica](remoteapp-bandwidthguidelines.md). Como es posible que el consumo por kilómetro varíe, debe ejecutar sus propias pruebas si *puede* .
> 
> 

## <a name="hello-usage-tests"></a>pruebas de uso de Hola
Cada una de estas pruebas se ejecutan durante distintos períodos de tiempo y prueban diferentes funciones y características que consumen ancho de banda de red. Recuerde la combinación de hello toochoose de prueba que mejor coincida con los usuarios individuales de la empresa.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>PowerPoint executivo/complejo: ejecución entre 1000 y 900 segundos
Un usuario presenta entre 45 y 50 diapositivas de alta fidelidad mediante Microsoft Office PowerPoint en modo de pantalla completa. diapositivas de Hello deben contener imágenes, las transiciones (con animaciones) y fondos con degradado de color que son típicos de su empresa. usuario de Hello debe dedicar al menos 20 segundos en cada diapositiva.

Este escenario crea el tráfico por ráfagas, cuando realiza una transición una diapositiva toohello siguiente diapositiva de presentación de Hola.

### <a name="simple-powerpoint---run-for-620-seconds"></a>PowerPoint simple: ejecución durante aprox. 620 segundos
Un usuario presenta un archivo sencillo de PowerPoint de aproximadamente 30 diapositivas mediante Microsoft Office PowerPoint en modo de pantalla completa. diapositivas de Hello consumen más texto que en escenario de hello PowerPoint ejecutivo o que son complejas y tienen más sencillo fondos e imágenes (diagramas negros). 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer: ejecución durante aprox. 250 segundos
Un usuario examina web hello mediante Internet Explorer. usuario de Hello examina y se desplaza a través de una combinación de texto, imágenes naturales y algunos de los diagramas esquemáticos. Hola páginas web almacenadas en Hola de unidad de disco local del servidor de Host de sesión de escritorio remoto (RD Session Host) Hola como un. Archivo MHT. usuario de Hola se desplaza con RE PÁG, AV PÁG, arriba y hacia abajo de claves, con distintos intervalos de cada clave o el tipo de desplazamiento:

    - Abajo: 250 pulsaciones de teclas cada 500 ms
    - Re Pág: 36 pulsaciones de teclas cada 1000 ms
    - Abajo: 75 pulsaciones de teclas cada 100 ms
    - Av Pág: 20 pulsaciones de teclas cada 500 ms
    - Hasta: 120 pulsaciones cada 300 ms

### <a name="pdf-document---simple---run-for-610-seconds"></a>Documento PDF - simple: ejecución durante aprox. 610 segundos
El usuario busca y lee un documento PDF de diversas maneras mediante Adobe Acrobat Reader. documento de Hello debe constar de varias fuentes de texto, tablas y gráficos simples. documento de Hello es 35-40 páginas. usuario de Hola se desplaza a través de dos tipos diferentes, con las versiones anteriores y reenvía en cuatro tamaños diferentes zoom (ajustar toopage, ajuste toowidth, 100% y otro de su elección). Hola zoom garantiza que se representará el texto hello (font) de diferentes tamaños. El desplazamiento es por medio de hello RE PÁG, AV PÁG, arriba y hacia abajo de claves, con distintos intervalos de cada desplazamiento.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>Documento PDF - mixto: ejecución durante aprox. 320 segundos
El usuario busca y lee un documento PDF de diversas maneras mediante Adobe Acrobat Reader. documento de Hello consta de imágenes de alta calidad (incluidos fotografías), tablas, gráficos simples y múltiples fuentes de texto. usuario de Hola se desplaza a través de dos tipos diferentes, con las versiones anteriores y reenvía en cuatro tamaños diferentes zoom (ajustar toopage, ajuste toowidth, 100% y otro de su elección). Hola zoom garantiza que se representará el texto hello (font) de diferentes tamaños. El desplazamiento es por medio de hello RE PÁG, AV PÁG, arriba y hacia abajo de claves, con distintos intervalos de cada desplazamiento.

### <a name="flash-video-playback---run-for-180-seconds"></a>Reproducción de vídeo Flash: ejecución durante aprox. 180 segundos
Un usuario ve un vídeo con codificación de Adobe Flash insertado en una página web. página web de Hola se almacena en la unidad de disco duro local de Hola de servidor de Host de sesión de escritorio remoto de Hola. Hola vídeo se reproduce en Internet Explorer mediante un reproductor incrustado de complemento.

En este escenario se emulan a los usuarios que ven páginas web con contenido enriquecido que incluye contenido multimedia. La mayoría de los datos de hello debe a bo a través de VOBR.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Escritura remota en Word: ejecución durante aprox. 1800 segundos
Un usuario escribe un documento en una sesión de RDP. Pulsaciones de teclas se envían desde el cliente hello por documento de tooa de sesión RDP de hello en Microsoft Word ejecuta en una sesión remota de Hola. Hola escribe tasa es un carácter cada 250 ms (total 7050 caracteres). 

Este es uno de los escenarios más comunes de Hola para un trabajador del conocimiento. Este escenario comprueba la capacidad de respuesta de Hola de un usuario que escribe en un procesador de trabajo modernas. Este escenario es confidencial tooeven pequeños cambios en el uso de ancho de banda.

## <a name="tracking-hello-test-results"></a>Seguimiento de resultados de pruebas de Hola
Puede usar Hola siguientes escenarios de tabla tooevaluate hello en su entorno. datos de Hello proporcionados a continuación tienen solo fines ilustrativos: puede ser considerablemente diferente de lo que se muestra. 

Para simplificar, se supone que todos los escenarios se prueban utilizando la resolución de pantalla de hello mismo 1920 x 1080 píxeles y transportes TCP en una red con latencia (un retardo) inferior a 200 ms y red vibración en hello 120 ms + marca de aproximadamente un 1%.

Acerca de la tabla de hello:

* **Promedio de experiencia** contiene el ancho de banda de red de Hola donde la productividad del usuario no es considerablemente afectada, pero no excluye los problemas de vídeo o audio ocasionales. sistema de Hello es capaz de toorecover rápidamente aprovechando las ventajas de lógica dinámica Hola. Hola ancho de banda estimaciones intento tooguarantee Hola calidad de la red de la experiencia del usuario Hola.
  * **Problemas apreciables (punto de interrupción)** contiene el ancho de banda de red de Hola donde los usuarios podrían observar problemas importantes en su experiencia y su productividad se ve afectada durante períodos de tiempo puede medir. En este momento algoritmos RDP Hola se esfuerzan por y no pueden garantizar la calidad del usuario de saludo de la experiencia a causa de ancho de banda de red son insuficientes.
  * **Se recomienda** contiene el ancho de banda de red de hello recomendado para buena o excelente experiencia. Es normalmente un paso superior valor hello en hello correspondientes **promedio experiencia** columna.
  * **Notas** se incluyen observaciones y comentarios.

| Prueba | Experiencia promedio | Problemas perceptibles (punto de interrupción) | Ancho de banda de red recomendado | Notas |
| --- | --- | --- | --- | --- |
| PPT ejecutivo/complejo |10 MB/s |1 MB/s |>10 MB/s, 100 MB/s (preferible) |A 1 MB/s se pierden muchas animaciones |
| PPT simple |5 MB/s |256 KB/s |10 MB/s |En 256 KB/seg. de carga con retraso notable diapositivas de Hola |
| Internet Explorer |10 MB/s |1 MB/s |>10 MB/s, 100 MB/s (preferible) |A 1 MB/s, los vídeos web son borrosos y se entrecortan, el desplazamiento rápido presenta problemas |
| PDF simple |1 MB/s |256 KB/s |5 MB/s |A 256 KB/s se tarda un tiempo página de hello tooload |
| PDF mixto |1 MB/s |256 KB/s |5 MB/s |A 256 KB/s página Hola lleva una cantidad considerable de tooload de tiempo |
| Reproducción de vídeo Flash |10 MB/s |1 MB/s |>10 MB/s, 100 MB/s (preferible) |A 1 MB/s Hola vídeo se muestra granulado y se quitan algunos marcos |
| Escritura remota en Word |256 KB/s |128 KB/s |1 MB/s |A 256 KB/s usuario puede observar Hola tiempo que transcurre entre las pulsaciones de teclas |

tooevaluate Hola ancho de banda por usuario, cree una combinación de Hola por encima de los escenarios y proporción correspondiente de Hola de ancho de banda de red necesario. Seleccionar un número más alto de hello necesario para los escenarios. Puesto que los usuarios no utilizan casi nunca sistema Hola por sí sola, tenga en cuenta algunas reserva para los usuarios que trabajan simultáneamente en Hola la misma red.

## <a name="learn-more"></a>Más información
* [Cálculo aproximado del uso del ancho de banda de red de Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp: ¿cómo funcionan el ancho de banda de red y la calidad de la experiencia conjuntamente?](remoteapp-bandwidthexperience.md)
* [Ancho de banda de red de Azure RemoteApp: directrices generales (si no puede probarlo por sí mismo)](remoteapp-bandwidthguidelines.md)

