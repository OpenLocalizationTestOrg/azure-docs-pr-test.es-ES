---
title: "requisitos previos para la creación de un servicio de datos para hello Marketplace aaaTechnical | Documentos de Microsoft"
description: "Comprender los requisitos de hello para la creación de un servicio de datos toodeploy y vender en hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Técnicos requisitos previos para la creación de un servicio de datos ofrecen para hello Azure Marketplace
> [!IMPORTANT]
> **En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.** Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners). Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Leer proceso Hola exhaustivamente antes de comenzar y comprender dónde y por qué se realiza cada paso. Tanto como sea posible, debe preparar la información de su empresa y otros datos, descargue las herramientas necesarias, o quiere crear componentes técnicos antes de comenzar el proceso de creación de hello oferta.

Debe tener Hola siguientes elementos listos antes de comenzar el proceso de hello:

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>Tomar una decisión sobre qué tecnología será toopublish usa su oferta de servicio de datos
Un editor puede decidir entre varias tecnologías al publicar un servicio de datos en Azure Marketplace. Hola principales tecnologías que sean compatibles que se describe a continuación. Sin importar qué tecnología es hello toopublish usa el servicio de datos, por el usuario final de hello consume datos de Hola a través de hello **fuente de OData** expuestos por el servicio de Azure Marketplace. Para encontrar toda la información acerca del servicio de OData, consulte la página [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>Base de datos de SQL Azure
Tener el conjunto de datos listo en SQL Azure es responsabilidad del publicador. Necesitará toosubscribe tooAzure, aprovisionar el tamaño adecuado de la base de datos y cargar los datos en la base de datos de SQL Azure. Publicador también es responsable tookeep sus datos siempre está actualizadas. Para obtener más información acerca de la suscripción tooAzure Services puede encontrar en [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

Al mover los datos de hello en SQL Azure, puede exponer hello Azure Marketplace tablas y vistas. Hola publicador puede especificar qué tablas/vistas y columnas se toohello expuesto por el usuario final. Proveedor de contenido adicional de hello también puede especificar qué columnas pueden ser consultadas por el usuario final de Hola y las que solo se devuelven en la carga de Hola. Esto proporciona un alto grado de flexibilidad sobre qué debe exponerse Hola base de datos. Las columnas que se pueden consultar necesitan toobe respaldado por uno o más índices de base de datos.

## <a name="rest-based-web-service"></a>Servicio web basado en REST
Protocolo admitido: **HTTPS solo**

Servicios basada en REST existentes pueden exponerse a través de hello Azure Marketplace. Porque el conjunto de datos de hello siempre toohello expuesto por el usuario final como una fuente OData, Hola servicio de Azure Marketplace necesita toobe pueda toomap Hola tooa servicio OData en función de servicio. toodo para que los puntos de conexión basada en REST de hello necesitan tooexpose todos los parámetros como parámetros HTTP.

carga de Hello debe toobe en un formulario que se pueden asignar a una respuesta ATOM. Por lo tanto, respuesta de hello de servicios de hello necesita toobe en formato XML y solo puede contener un elemento repetido que contiene los valores de la carga de hello (por ejemplo, conjunto de registros). Hola servicio de Azure Marketplace asignará Hola repetir nodo toohello nodo de entrada de los valores de carga ATOM y hello en nodos de propiedad en el nodo de entrada de Hola.

Información de autorización (por ejemplo, API, clave, etc. símbolo (token), autenticación) debe toobe proporcionado como un parámetro HTTP o en el encabezado HTTP de hello (pares clave-valor): también se admite la autenticación básica. Una clave válida debe toobe proporcionado y todas las solicitudes a través de Azure Marketplace se que se realizan a través de esa clave. Usuario supervisión y facturación se produce en la capa de hello Azure Marketplace.

Errores devueltos por el servicio de hello necesitan toobe asignada a códigos de estado HTTP. En caso de servicio de hello devuelva un XML que contiene el error de hello estos va toobe asignada por códigos de estado del servicio tooHTTP de hello Azure Marketplace.

## <a name="soap-based-web-services"></a>Servicios web basados en SOAP
Protocolo: **HTTPS solo**

requisitos de Hello son Hola mismo como en la sección de servicio de hello basada en REST. Hola única diferencia es que también se pueden proporcionar los parámetros en un cuerpo XML que se está publicando servicio del Editor de toohello con todas las solicitudes realizadas a través de Azure Marketplace. Esto significa que usuario HTTP parámetros Hola presta en hello front-end se está traduciendo en elementos XML de un documento XML que se está publicando con hello solicitud toohello contenido del servicio web del proveedor.

## <a name="odata-based-web-services"></a>Servicios web basados en OData
Protocolo: **HTTPS solo**

Pueden exponer datos como un tooAzure de servicio de OData Marketplace. sistema Hello es continuo toopass servicio Hola a través y reemplaza raíz Hola del servicio de hello con la raíz del servicio de Azure Marketplace Hola – tooensure vaya todas las llamadas subsiguientes a través de Azure Marketplace.

Servicios de OData solo no es necesario toogo en una base de datos back-end de Hola. OData admite cualquier tipo de almacenamiento o business lógica toodrive Hola un servicio.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha revisado los requisitos previos de Hola y se ha completado tareas necesarias de hello, puede avanzar con hello crear su oferta de servicio de datos como Hola detallada en [Guía de publicación de servicio de datos](marketplace-publishing-data-service-creation.md).

O bien, si desea que tooreview Hola proceso general y artículos respectivos Hola para cada publicación fases de hello, visite artículo hello [Introducción: cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
