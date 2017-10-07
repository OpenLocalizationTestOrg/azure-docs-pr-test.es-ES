---
title: "implementación de Mobile Engagement aaaAzure para una aplicación multimedia"
description: "Medios aplicación escenario tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>Implementación de Mobile Engagement con una aplicación de medios
## <a name="overview"></a>Información general
John es un encargado de proyectos móviles para una gran empresa de medios. Acaba de lanzar una nueva aplicación con un número muy elevado de descargas. Ha cumplido sus objetivos en lo que respecta a las descargas, pero la rentabilidad de la inversión (ROI) por usuario no los cumple. 

John ya ha identificado por qué su ROI es demasiado baja. Los usuarios suelen dejan de usar la aplicación después de solo 2 semanas y la mayoría no regresa nunca. Quiere que la retención de hello tooincrease de su aplicación.

Después de realizar algunas pruebas inicial, que ha aprendido al involucre a sus usuarios con las notificaciones de inserción, suele toocontinue con su aplicación. También a los usuarios que estaban inactivos a menudo devolverá toohello aplicación dependiendo de las notificaciones que envía. Juan decide tooinvest en algún tipo de programa de interacción de su aplicación que usa la selección avanzada de destinatarios con las notificaciones de inserción.

Juan recientemente ha leído hello [Azure Mobile Engagement - Guía de introducción a los procedimientos recomendados](mobile-engagement-getting-started-best-practices.md) y ha decidido recomendaciones de hello tooimplement de guía de Hola.

## <a name="objectives-and-kpis"></a>Objetivos y KPI
Las partes interesadas clave de la aplicación de John se reúnen. Se generan ingresos a partir de anuncios mientras los usuarios consumen sus medios. Si aumenta el contenido consumido por usuario, John aumenta sus ingresos. Todos los equipos acuerdan un objetivo principal: tooincrease ventas de los anuncios en un 25%. Crear unidad y los indicadores clave de rendimiento (KPI) empresariales toomeasure este objetivo

* Número de anuncios pulsados por usuario
* Cantidad de páginas de artículos visitadas (por usuario/por sesión/por semana/por mes…)
* Cuáles son las categorías favoritas

Tras la reunión de John con las personas interesadas clave, ha definido sus KPI de negocio. Este sigue parte 1 de hello [Azure Mobile Engagement - Guía de introducción a los procedimientos recomendados](mobile-engagement-getting-started-best-practices.md). 

A continuación, crea Hola después tooensure de contratación KPI que se alcancen los objetivos:

* Supervisar retención en hello siguientes intervalos: diaria, semanal, bisemanal y mensuales.
* Recuentos de usuarios activos
* clasificación de aplicación Hello en la aplicación hello almacena

En función de las recomendaciones del equipo de TI de hello, Hola siguientes KPI técnica se agregaron hello tooanswer siguientes preguntas:

* ¿Cuál es la ruta de acceso de los usuarios (qué página visitan, cuánto tiempo pasan los usuarios en ella)?
* ¿Número de bloqueos o errores encontrados por sesión?
* ¿Qué versiones de sistema operativo ejecutan mis usuarios?
* ¿Qué es el tamaño medio de Hola de pantalla para Mis usuarios?
* ¿Qué tipo de conexiones a Internet tienen mis usuarios?

Para cada KPI, clasifica los datos de hello necesarios y lo registra en ubicación correcta de hello de la guía.

## <a name="engagement-program-and-integration"></a>Programa de compromiso e integración
Ahora que John ha terminado de definir sus KPI, comienza la fase de estrategia de compromiso y define cuatro programas de compromiso y sus objetivos: ![][1]

Después, John profundiza aún más y detalla las notificaciones push para cada programa. La definición de la notificación push consta de cinco elementos:

1. Objetivo: ¿cuál es el objetivo de Hola de notificación de Hola
2. ¿Cómo se llega al objetivo de Hola
3. Destino: quién recibirá notificación de hello?
4. Contenido: ¿Qué es una redacción Hola y el formato de Hola de notificación de hello (en App/Out de aplicación)
5. Cuando: ¿qué es Hola mejor toosend momento esta notificación de inserción
   
    ![][2]

Para obtener más información, consulte toohello [guías](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).

Según toohello parte 2 de notas del producto Hola que Juan utiliza toodefine de la sección de destino de los datos que tiene toocollect y escribe su etiqueta Plan junto con soluciones de TI equipo tooimplement Hola. Después de una semana de implementación y pruebas de aceptación del usuario, John finalmente lanza sus programas.

## <a name="program-results"></a>Resultados de los programas
Cuatro meses después, John evalúa el rendimiento de los programas. Bienvenida programa Hola y Hola programa semanal están cumpliendo los objetivos. reduce el número de saludo del usuario con sesión sólo una, se usan más características de la aplicación hello y Hola número de conexiones por semana se ha duplicado.

Hola **programa inactiva** está ayudando a Juan a entender las tendencias de usuario. Parece que el 15% de los usuarios inactivos de hello vuelven a estar toohello aplicación. Sin embargo, la mayoría no permanecen activos más de 1 mes. John prevé una posible optimización de esta secuencia con notificaciones adicionales y mayor selección de contenido.

Hola **programa Discover** no funciona bien. Aumenta entre las ventas, pero no hay suficientes tooreach sus objetivos. Juan identifica que no tiene suficientes datos toomake pertinentes como destino y proponer contenido adecuado. Abandona este programa y se centra en enviar "notificaciones push editoriales" con Azure Mobile Engagement. Sus periodistas ya tienen un notificaciones de inserción CMS solución toosend y no desean toochange.

Juan decide toouse Hola API de cobertura que es una API de REST de HTTP que permite administrar campañas sin necesidad de interfaz de AZME Web toouse. Con este enfoque Juan puede recopilar datos de Hola que necesita y permitir que los escritores tookeep mediante Hola CMS solución.

tooensure que funciona la característica correctamente, Juan solicita toobe del equipo de TI supervisar en hello siguientes puntos:

1. **Sistemas operativos** : todas ellas tienen sus propios notificaciones de inserción de tooadministrate de reglas, por lo que John decide toolist todos los casos y comprueba si Hola API controlarla.
   Por ejemplo: Sistema de inserción Android permite panorama general que no es el caso de hello con iOS.
2. **Período de tiempo**: Juan desea una API, que establece el período de tiempo de Hola y establece un toocampaigns final. Quiere que los usuarios de toopreserve desde cualquier notificación perturbador masivo.
3. **Categorías**: el equipo de marketing prepara la plantilla para cada tipo de alerta. Juan solicita tooset categorías de equipo de TI dentro de hello API.

Tras varias pruebas, John está satisfecho. API de toothis gracias, periodistas aun así pueden enviar notificaciones de inserción con sus CMS y Azure Mobile Engagement recopila todos los datos de comportamientos para ellos

Después de estos cuatro primeros meses, los resultados reflejan un buen rendimiento general e inspiran confianza en John y la junta, la ROI por usuario ha aumentado en un 15% y las ventas móviles representan un 17,5% del total, un aumento del 7,5% en solo cuatro meses.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
