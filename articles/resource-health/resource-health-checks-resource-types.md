---
title: "aaaSupported tipos de recursos a través de estado de los recursos de Azure | Documentos de Microsoft"
description: "Tipos de recursos que se admiten a través de Azure Resource Health"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: a37d5c33f6ef6fdfbce0daf392bc7fa57853c7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Tipos de recursos y comprobaciones de estado en Azure Resource Health
A continuación se muestra una lista completa de todas las comprobaciones de hello ejecutadas a través de mantenimiento de recursos por tipos de recursos.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Están todos los nodos de la memoria caché de Hola y ejecutar?</li><li>¿Hola caché pueden alcanzar desde dentro de centros de datos de hello?</li><li>¿Tiene Hola que caché alcanza el número máximo de Hola de conexiones?</li><li> ¿Caché Hola agotó su memoria disponible? </li><li>¿Hola caché tiene un gran número de errores de página?</li><li>¿Se Hola caché con mucha carga?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Comprobaciones ejecutadas|
|---|
|<ul> <li>¿Cualquiera de los puntos de conexión de Hola se detuvo, mal configurada o eliminada?</li><li>¿Es accesible para las operaciones de configuración de red CDN portal complementario de hello?</li><li>¿Son hay problemas de entrega continua con hello puntos de conexión CDN?</li><li>¿Pueden los usuarios cambiar configuración Hola de sus recursos de red CDN?</li><li>¿Están propagando cambios de configuración a velocidad de hello esperada?</li><li>¿Pueden administrar los usuarios configuración de red CDN Hola mediante Hola portal de Azure, PowerShell o API de hello?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Depende de servidor de host de Hola y ejecutar?</li><li>¿Arranque de sistema operativo de host de hello ha completado?</li><li>¿Contenedor de máquina virtual de hello aprovisionado y encendida?</li><li>¿Hay conectividad de red entre el host de Hola y cuenta de almacenamiento de hello?</li><li>¿Hola arranque de sistema operativo invitado de hello ha completado?</li><li>¿Hay mantenimiento planeado en curso?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Cuenta de hello pueden alcanzar desde dentro de centros de datos de hello?</li><li>¿Se Hola cognitivos proveedor de recursos de servicios disponibles?</li><li>¿Se Hola cognitivos servicio disponible en la región adecuada de hello?</li><li>¿Puede leer operaciones pueden realizarse en la cuenta de almacenamiento de Hola que contiene metadatos de recursos de hello?</li><li>¿Se ha alcanzado la cuota de llamada de API de hello?</li><li>¿Ha alcanzado el límite de lectura de hello API llamadas?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.compute/virtualmachines
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Servidor de hello hospeda esta máquina virtual una y ejecutando?</li><li>¿Arranque de sistema operativo de host de hello ha completado?</li><li>¿Contenedor de máquina virtual de hello aprovisionado y encendida?</li><li>¿Hay conectividad de red entre el host de Hola y cuenta de almacenamiento de hello?</li><li>¿Hola arranque de sistema operativo invitado de hello ha completado?</li><li>¿Hay mantenimiento planeado en curso?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Pueden los usuarios enviar trabajos de análisis de tooData Lake en Hola región?</li><li>¿Hacer la región de Hola de ejecución y se completa correctamente en trabajos básica?</li><li>¿Pueden enumerar los usuarios elementos de catálogo en la región de hello?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Pueden cargar los usuarios datos tooData Lake almacén en la región de hello?</li><li>¿Pueden a los usuarios descargar datos de almacén de Data Lake en la región de hello?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Se han producido las solicitudes de base de datos o una colección no sirven debido a falta de disponibilidad del servicio de documentos de tooa?</li><li>¿Se ha producido ninguna solicitud de documento no sirven debido a falta de disponibilidad del servicio de documentos de tooa?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.network/connections
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Está conectado el túnel VPN de hello?</li><li>¿Hay conflictos de configuración de conexión de hello?</li><li>¿Las claves previamente compartidas Hola configuradas correctamente?</li><li>¿Dispositivo de hello VPN local se encuentra accesible?</li><li>¿Hay discrepancias en la directiva de seguridad de IPSec/IKE Hola?</li><li>¿Es la conexión de VPN de S2S de hello aprovisionado correctamente o en estado de error?</li><li>¿Es la conexión de red virtual a red virtual de hello aprovisionado correctamente o en estado de error?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Es accesible desde la puerta de enlace VPN de Hola Hola internet?</li><li>¿Se Hola puerta de enlace VPN en modo de suspensión?</li><li>¿Está ejecutando Hola servicio VPN en puerta de enlace de hello?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Comprobaciones ejecutadas|
|---|
|<ul><li> ¿Se pueden realizar operaciones de tiempo de ejecución como registro, la instalación o envío en el espacio de nombres de hello?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Depende de los sistemas operativos de host de Hola y ejecutar?</li><li>¿Es accesible desde fuera de centro de datos de Hola Hola workspaceCollection?</li><li>¿Se Hola proveedor de recursos de Power BI disponible?</li><li>¿Se Hola PowerBI Service disponible en la región adecuada de hello?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Se pueden realizar operaciones de diagnóstico en el clúster de hello?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Comprobaciones ejecutadas|
|---|
|<ul><li> ¿Ha habido una base de datos de los inicios de sesión toohello?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Son todos los hosts de Hola donde se ejecuta una y ejecutar trabajo Hola?</li><li>¿Era Hola trabajo no se puede toostart?</li><li>¿Hay actualizaciones del runtime en curso?</li><li>¿Es trabajo hello en el estado esperado (por ejemplo en ejecución o detenido por el cliente)?</li><li>¿Hello trabajo encontró fuera de las excepciones de memoria?</li><li>¿Hay actualizaciones del proceso programado en curso?</li><li>¿Se Hola Administrador de ejecución (plan de control) disponible?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Depende de servidor de host de Hola y ejecutar?</li><li>¿Se ejecuta Internet Information Services (IIS)?</li><li>¿Se está ejecutando el equilibrador de carga de hello?</li><li>¿Hola Plan del servicio Web pueden alcanzar desde dentro de centros de datos de hello?</li><li>¿Está Hola almacenamiento cuenta hospedaje Hola contenido de los sitios de la granja de servidores de hello disponible?</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.web/sites
|Comprobaciones ejecutadas|
|---|
|<ul><li>¿Depende de servidor de host de Hola y ejecutar?</li><li>¿Se ejecuta Internet Information Server?</li><li>¿Se está ejecutando el equilibrador de carga de hello?</li><li>¿Hola aplicación Web se puede acceder desde dentro de centros de datos de hello?</li><li>¿Cuenta de almacenamiento de hello hospeda contenido de sitio de hello disponible?</li></ul>|

Consulte estos toolearn recursos más información sobre el estado de los recursos:
-  [Estado de los recursos tooAzure Introducción](Resource-health-overview.md)
-  [Preguntas más frecuentes acerca de Azure Resource Health](Resource-health-faq.md)

