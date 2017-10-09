---
title: aaaCreate un concentrador de eventos de Azure | Documentos de Microsoft
description: Crear un espacio de nombres de los centros de eventos de Azure y un concentrador de eventos mediante Hola portal de Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>Crear un espacio de nombres de los centros de eventos y un concentrador de eventos mediante Hola portal de Azure

## <a name="create-an-event-hubs-namespace"></a>Creación de un espacio de nombres de Event Hubs
1. Inicie sesión en toohello [portal de Azure][Azure portal]y haga clic en **New** en hello parte superior izquierda de la pantalla de bienvenida.
1. Haga clic en **Internet de las cosas** y, luego, en **Event Hubs**.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. Hola **crear espacio de nombres** hoja, escriba un nombre de espacio de nombres. sistema de Hello comprueba inmediatamente toosee si Hola nombre está disponible.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. Después de realizar el nombre de espacio de nombres de hello seguro está disponible, elija Hola tarifa (básico o estándar). Además, elija una suscripción de Azure, el grupo de recursos y la ubicación en el recurso que hello toocreate. 
1. Haga clic en **crear** el espacio de nombres de toocreate Hola. Puede que tenga toowait unos minutos para los recursos Hola Hola sistema toofully aprovisionar.
2. En la lista de portales de Hola de espacios de nombres, haga clic en hello que acaba de crear espacio de nombres.
2. Haga clic en **Directivas de acceso compartido** y después en **RootManageSharedAccessKey**.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Haga clic en Hola de hello copia botón toocopy **RootManageSharedAccessKey** Portapapeles de toohello de cadena de conexión. Guarde esta cadena de conexión en una ubicación temporal, como el Bloc de notas, toouse más tarde.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>Creación de un centro de eventos

1. En la lista de espacio de nombres de los centros de eventos de hello, haga clic en el espacio de nombres de hello recién creado.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. En la hoja de espacio de nombres de hello, haga clic en **centros de eventos**.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. En la parte superior de Hola de hoja de hello, haga clic en **agregar concentrador de eventos**.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. Escriba el nombre del centro de eventos y, luego, haga clic en **Crear**.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

Ahora se crea el centro de eventos y de que las cadenas de conexión de Hola que necesita toosend y recibe eventos.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de los centros de eventos, visite estos vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Información general de la API de Event Hubs](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/