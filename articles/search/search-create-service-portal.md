---
title: "un servicio de búsqueda de Azure en el portal de hello aaaCreate | Documentos de Microsoft"
description: "Aprovisionar un servicio de búsqueda de Azure en el portal de Hola."
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>Crear un servicio de búsqueda de Azure en el portal de Hola

Este artículo explica cómo toocreate o aprovisionar una búsqueda de Azure service en el portal de Hola. Para obtener instrucciones de PowerShell, consulte [Administración del servicio Azure Search con PowerShell](search-manage-powershell.md).

## <a name="subscribe-free-or-paid"></a>Suscripción (gratuita o de pago)

[Abrir una cuenta de Azure gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) y usar tootry de créditos gratuitos a los servicios de Azure de pago. Después de que se agoten los créditos, mantener la cuenta de hello y continuar servicios de Azure gratuita de toouse, como sitios Web. Nunca se cobra su tarjeta de crédito a menos que cambiar la configuración y pida toobe cobrado explícitamente.

Opcionalmente, [puede activar los beneficios de suscriptores de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Una suscripción a MSDN le proporciona créditos todos los meses que puede usar para servicios de Azure de pago. 

## <a name="find-azure-search"></a>Búsqueda de Azure Search
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en hello más el signo ("+") en hello esquina superior izquierda.
3. Seleccione **Web y móvil** > **Azure Search**.

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>Servicio de nombre hello y punto de conexión de dirección URL

Un nombre de servicio es parte del punto de conexión de dirección URL de hello con la que se emiten llamadas a la API. Escriba el nombre del servicio en hello **URL** campo. 

Requisitos de nombre de servicio:
   * Entre 2 y 60 caracteres de longitud.
   * Letras minúsculas, números o guiones ("-").
   * ningún guión ("-") como Hola 2 primeros caracteres o último carácter único
   * Sin guiones consecutivos ("--").

## <a name="select-a-subscription"></a>Selección de una suscripción
Si tiene más de una suscripción, elija una que también tenga servicios de almacenamiento de datos o archivos. Búsqueda de Azure puede detectar automáticamente almacenamiento de tabla de Azure y Blob, base de datos SQL y base de datos de Azure Cosmos para indizar a través de *indizadores*, pero solo para los servicios en hello misma suscripción.

## <a name="select-a-resource-group"></a>Selección de un grupo de recursos
Un grupo de recursos es una colección de servicios y recursos de Azure que se usan juntos. Por ejemplo, si está utilizando búsqueda de Azure tooindex una base de datos SQL, ambos servicios deben formar parte del programa Hola mismo grupo de recursos.

> [!TIP]
> Eliminación de un grupo de recursos, también elimina servicios Hola dentro de él. Para los proyectos de prototipo utilizando varios servicios, colocar todas ellas en hello mismo grupo de recursos facilita el Liberador de espacio después de proyecto de Hola. 

## <a name="select-a-hosting-location"></a>Selección de una ubicación de hospedaje 
Como un servicio de Azure, la búsqueda de Azure se pueden hospedar en centros de datos Hola mundo. Tenga en cuenta que los [precios pueden variar](https://azure.microsoft.com/pricing/details/search/) según la región geográfica.

## <a name="select-a-pricing-tier-sku"></a>Selección de un plan de tarifa (SKU)
[Búsqueda de Azure se ofrece actualmente en varios planes de tarifa](https://azure.microsoft.com/pricing/details/search/): Gratis, Básico y Estándar. Cada plan tiene su propia [capacidad y sus propios límites](search-limits-quotas-capacity.md). Consulte [Selección SKU o plan de tarifa](search-sku-tier.md) para obtener instrucciones.

En este tutorial, que hemos elegido nivel estándar de Hola para nuestro servicio.

## <a name="create-your-service"></a>Creación del servicio

Recuerde toopin el panel de toohello de servicio para facilitar el acceso siempre que inicie sesión.

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>Escalar el servicio
Puede tardar unos toocreate minutos un servicio (15 minutos o más en función del nivel de hello). Después de aprovisionar el servicio, se puede escalar toomeet sus necesidades. Debido a que decidió nivel estándar de hello para el servicio de búsqueda de Azure, puede escalar el servicio en dos dimensiones: réplicas y particiones. Ha elegido nivel básico de hello, solo puede agregar réplicas. Si se ha aprovisionado el servicio gratuito de hello, escala no está disponible.

***Las particiones*** permitir que el servicio toostore y la búsqueda a través de varios documentos.

***Réplicas*** permitir su toohandle de servicio más carga de consultas de búsqueda.

> [!Important]
> Un servicio debe tener [2 réplicas para SLA de solo lectura y 3 réplicas para SLA de lectura y escritura](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

1. Vaya tooyour hoja de servicio de búsqueda en hello portal de Azure.
2. En el panel de navegación de la izquierda de hello, seleccione **configuración** > **escala**.
3. Utilice hello slidebar tooadd réplicas o particiones.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> Cada nivel tiene diferentes [límites](search-limits-quotas-capacity.md) número total de Hola de unidades de búsqueda que se permiten en un único servicio (réplicas * particiones = Total de unidades de búsqueda).

## <a name="when-tooadd-a-second-service"></a>Cuando un segundo servicio tooadd

La gran mayoría de los clientes usar un solo servicio proporciona en un nivel que proporciona hello [haga equilibrio de recursos](search-sku-tier.md). Un servicio puede hospedar varios índices, asunto toohello [límites máximos de capa de hello selecciona](search-capacity-planning.md), con cada índice aislado de la otra. En la búsqueda de Azure, las solicitudes solo pueden ser dirigido tooone índice, minimizar la posibilidad de hello accidental o intencionado de recuperación de datos de otros índices de hello mismo servicio.

Aunque la mayoría de los clientes usa un solo servicio, redundancia de servicio puede ser necesario si los requisitos operativos de hello siguientes:

+ Recuperación ante desastres (interrupción del centro de datos). Búsqueda de Azure no proporciona la conmutación por error instantánea en caso de hello de una interrupción. Para obtener recomendaciones e instrucciones, consulte el artículo sobre [administración de servicios](search-manage.md).
+ La investigación de modelado de la arquitectura multiempresa ha determinado que servicios adicionales es diseño óptimo de Hola. Para obtener más información, consulte el artículo sobre [diseño para multiempresa](search-modeling-multitenant-saas-applications.md).
+ Para las aplicaciones implementadas globalmente, podría necesitar una instancia de la búsqueda de Azure en varios toominimize de latencia de las regiones de tráfico internacional de la aplicación.

> [!NOTE]
> En Azure Search, no puede separar las cargas de trabajo de indización y consultas; por lo tanto, nunca podría crear varios servicios para las cargas de trabajo segregadas. Un índice siempre se consulta en el servicio de hello en donde se ha creado (no se puede crear un índice en un servicio y cópielo tooanother).
>

No se requiere un segundo servicio para lograr alta disponibilidad. Alta disponibilidad para las consultas se logra al utilizar 2 o más réplicas de Hola mismo servicio. Las actualizaciones de réplicas son secuenciales, lo que significa que, al menos, una es operativa cuando se implementa una actualización de servicio. Para obtener más información, consulte [Acuerdos de Nivel de Servicio](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## <a name="next-steps"></a>Pasos siguientes
Después de aprovisionar un servicio de búsqueda de Azure, estás listo demasiado[definir un índice](search-what-is-an-index.md) para que pueda cargar y buscar los datos.

tooaccess Hola servicio de código o script, proporcione la dirección de URL de hello (*nombre-servicio*. search.windows.net) y una clave. Las claves de administrador conceden acceso completo; las claves de consulta conceden acceso de solo lectura. Vea [cómo toouse búsqueda de Azure en .NET](search-howto-dotnet-sdk.md) tooget iniciado.

Consulte [Compilación y consulta del primer índice](search-get-started-portal.md) para obtener un tutorial rápido basado en Azure Portal.

