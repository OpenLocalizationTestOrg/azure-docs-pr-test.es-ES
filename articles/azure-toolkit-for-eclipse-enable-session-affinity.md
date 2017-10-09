---
title: "uso de afinidad de la sesión de aaaEnable Hola Kit de herramientas de Azure para Eclipse"
description: "Obtenga información acerca de cómo tooenable sesión afinidad con hello Azure Toolkit for Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>Habilitar la afinidad de la sesión
Dentro de hello Azure Toolkit for Eclipse, puede habilitar afinidad de la sesión HTTP, o "sesiones permanentes", para sus roles. Hello siguiente imagen muestra hello **equilibrio de carga** la característica de afinidad de la sesión propiedades diálogo utiliza tooenable hello:

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>afinidad de la sesión de tooenable para el rol
1. Haga clic en función de hello en el Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **equilibrio de carga**.

2. Hola **propiedades de equilibrio de carga de WorkerRole1** cuadro de diálogo:

   a. Active **Habilitar afinidad de sesión HTTP (sesiones permanentes) para este rol**

   b. Para **toouse de extremo de entrada**, seleccione un extremo de entrada toouse, por ejemplo, **http (público: 80, private: 8080)**. Su aplicación debe usar este punto de conexión como su punto de conexión HTTP. Puede habilitar varios puntos de conexión para el rol, pero puede seleccionar solo una de ellas toosupport sesiones permanentes.

   c. Vuelva a compilar la aplicación.

Una vez habilitada, si tiene más de una instancia de rol, las solicitudes HTTP procedentes de un cliente en particular seguirán estando controladas por hello misma instancia de rol.

Hola Kit de herramientas Eclipse hace esto posible mediante la instalación de un módulo IIS especial llamado enrutamiento de solicitud de aplicaciones (ARR) en cada una de las instancias del rol. ARR vuelve a enrutar instancia de rol correspondiente de toohello de las solicitudes HTTP. Kit de herramientas de Hello vuelve a configurar automáticamente el punto de conexión de hello seleccionado para que el tráfico HTTP entrante hello es el primer software ARR de toohello enrutado. Kit de herramientas de Hello también crea un nuevo extremo interno que se toolisten configurado para el servidor de Java. Que es el punto de conexión de hello utilizado por ARR tooreroute Hola HTTP tráfico toohello rol correspondiente instancia. De esta manera, cada instancia de rol en la implementación de varias instancias actúa como un proxy inverso para todos los Hola otras instancias, lo que permite sesiones permanentes.

## <a name="notes-about-session-affinity"></a>Notas sobre la afinidad de sesión
* Afinidad de la sesión no funciona en el emulador de proceso de Hola. configuración de Hola se puede aplicar en el emulador de proceso de hello sin interferir con el proceso de compilación o ejecución de emulador de proceso, pero propia característica hello no funciona en el emulador de proceso de Hola.

* Al habilitar la afinidad de sesión dará como resultado un aumento en la cantidad de Hola de espacio en disco utilizado por la implementación en Azure, tal y como se descargarse e instalarse en las instancias del rol cuando se inicia el servicio en nube de Azure Hola software adicional.

* Hola tiempo tooinitialize cada rol tardará más tiempo.

* Un extremo interno, toofunction como un nuevo tráfico como se mencionó anteriormente, se agregarán.


## <a name="see-also"></a>Otras referencias
[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]

[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse] 

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
