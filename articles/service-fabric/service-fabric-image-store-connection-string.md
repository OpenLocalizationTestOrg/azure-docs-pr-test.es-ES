---
title: "cadena de conexión de almacén de imagen de Service Fabric aaaAzure | Documentos de Microsoft"
description: "Comprender la cadena de conexión de almacén de imágenes de Hola"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Comprender la configuración de hello ImageStoreConnectionString

En la parte de la documentación, se mencione brevemente existencia Hola de un parámetro de "ImageStoreConnectionString" sin describir lo que significa realmente. Y después de pasar por un artículo como [implementar y quitar aplicaciones con PowerShell][10], parece que todo lo que hacer es copiar y pegar Hola valor tal y como aparece en el manifiesto de clúster de Hola de destino de Hola clúster. Por lo que el valor de hello deben configurable por clúster, pero cuando se crea un clúster a través de hello [portal de Azure][11], no hay ningún tooconfigure opción esta configuración y sus siempre "fabric: ImageStore". ¿Cuál es el propósito de Hola de esta configuración?

![Manifiesto de clúster][img_cm]

Service Fabric comenzó como una plataforma para consumo interno de Microsoft por muchos equipos distintos, por lo que algunos aspectos de la misma son personalizables: Hola "Image Store" es un aspecto de este tipo. En esencia, Hola Image Store es un repositorio conectable para almacenar los paquetes de aplicaciones. Cuando la aplicación está implementada tooa nodo en clúster de hello, ese nodo descarga contenido de Hola de su paquete de aplicación de hello Image Store. Hola ImageStoreConnectionString es una configuración que incluye toda la información necesaria Hola para los clientes y nodos toofind Hola correcto almacén de imágenes para un clúster determinado.

Actualmente existen tres posibles tipos de proveedores de almacenes de imágenes y sus correspondientes cadenas de conexión son las siguientes:

1. Servicio de almacén de imágenes: "fabric:ImageStore"

2. Sistema de archivos: "file:[ruta de acceso al sistema de archivos]"

3. Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"

tipo de proveedor de Hello utilizada en producción es hello servicio de almacén de imágenes, que es un servicio de sistema persistente con estado que puede ver en el Explorador de Service Fabric. 

![Servicio de almacén de imágenes][img_is]

Hospedaje Hola almacén de imágenes en un servicio de sistema dentro del propio clúster Hola elimina dependencias externas de repositorio de paquetes de saludo y nos proporciona mayor control sobre una localidad Hola de almacenamiento. Mejoras futuras alrededor de hello Image Store son proveedor de almacén de imágenes de hello tootarget es probable que en primer lugar, si no exclusivamente. cadena de conexión de Hello para el proveedor de servicio de almacén de imágenes de hello no tiene ninguna información exclusiva desde Hola cliente ya está conectado toohello clúster de destino. cliente de Hello solo necesita tooknow que se deben usar los protocolos que se dirige a servicio de sistema de Hola.

proveedor de sistema de archivos de Hola se utiliza en lugar de hello servicio de almacén de imágenes para los clústeres en un equipo locales durante clúster de desarrollo toobootstrap Hola un poco más rápido. diferencia de Hello es generalmente pequeña, pero es una optimización útil para la mayoría de la gente durante el desarrollo. Hola de sus posibles toodeploy un cuadro local de un clúster con otros tipos de proveedor de almacenamiento, pero normalmente no hay ninguna razón toodo así porque no cambia el flujo de trabajo de desarrollo y pruebas de Hola Hola igual independientemente del proveedor. Distinto de este uso, los proveedores de sistema de archivos y almacenamiento de Azure de hello solo existen para la compatibilidad heredada.

Por lo que aunque hello ImageStoreConnectionString es configurable, por lo general simplemente utilizar Hola configuración predeterminada. Al publicar tooAzure a través de [Visual Studio][12], parámetro hello se establece automáticamente según corresponda. Para la implementación mediante programación tooclusters hospedado en Azure, cadena de conexión de hello siempre es "fabric: ImageStore". Aunque en caso de duda, siempre se puede comprobar su valor mediante la recuperación de manifiesto de clúster de Hola por [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), o [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). Probar de forma local y clústeres de producción siempre deben ser el proveedor de servicio de almacén de imágenes de Hola de toouse configurado así.

### <a name="next-steps"></a>Pasos siguientes
[Implementación y eliminación de aplicaciones con PowerShell][10]

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
