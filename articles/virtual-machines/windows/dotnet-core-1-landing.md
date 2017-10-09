---
title: "aaaAzure Windows Máquina Virtual DotNet Core Tutorial 1 | Documentos de Microsoft"
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 14d5f250-1f76-49d4-898f-07b58fd39e7c
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8df69c496f44acb02d8afc45695349ec1f558f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toowindows-virtual-machines"></a>Automatizar las implementaciones de aplicación tooWindows máquinas virtuales

Esta serie de cuatro partes detalla la implementación y configuración de recursos y aplicaciones de Azure mediante plantillas de Azure Resource Manager. En esta serie, una plantilla de ejemplo se implementa y Hola examinada de plantilla de implementación. objetivo de Hola de esta serie es tooeducate en la relación de hello entre recursos de Azure y tooprovide amplíe su experiencia en la implementación de plantillas de Azure Resource Manager totalmente integrada. En este documento se da por hecho que el usuario posee un nivel básico de conocimientos de Azure Resource Manager, por lo que, antes de iniciar este tutorial, debe familiarizarse con los conceptos de Azure Resource Manager.

## <a name="music-store-application"></a>Aplicación Music Store
ejemplo utilizado en esta serie de Hello es un .net aplicación Core simulando una tienda de música experiencia de compra. Esta aplicación puede ser implementado tooeither un sistema virtual Linux o Windows, muestra las implementaciones se han creado para ambos. aplicación Hello incluye una aplicación web y una base de datos SQL. Antes de leer artículos Hola de esta serie, implementar la aplicación hello mediante el botón de la implementación de Hola se encuentra en esta página. Cuando está completamente distribuido, hello arquitectura de aplicación / Azure parece Hola siguiente diagrama. 

plantilla de administrador de recursos del almacén de música de Hello puede encontrarse aquí, [plantilla de Windows de tienda de música](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)

![Aplicación Music Store](./media/dotnet-core-1-landing/music-store.png)

Cada uno de estos componentes, incluidos Hola asociar plantilla JSON se examina en hello siguientes cuatro artículos.

* [**Arquitectura de la aplicación** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : componentes de la aplicación, como sitios web y bases de datos necesitan toobe hospedada en recursos del equipo de Azure como máquinas virtuales y bases de datos SQL de Azure. Este documento le guía a través de la necesidad de cálculo de asignación, tooAzure recursos e implementación de estos recursos a una plantilla de Azure Resource Manager. 
* [**Acceso y seguridad** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : cuando se hospedan aplicaciones de Azure, es necesario tooconsider cómo se tiene acceso a la aplicación hello y cómo acceder a componentes de aplicación diferentes entre sí. Este documento detalla proporcionar y protección de aplicación de internet access tooan y acceso entre componentes de la aplicación.
* [**Disponibilidad y escalabilidad** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : disponibilidad y escalabilidad, consulte toohello aplicaciones capacidad toostay ejecutándose durante el tiempo de inactividad de la infraestructura y Hola capacidad tooscale demanda de las aplicaciones toomeet recursos de proceso. Este documento detalles Hola los componentes necesitan toodeploy una carga equilibrada y aplicación de alta disponibilidad.
* [**Implementación de aplicaciones** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) : al implementar aplicaciones en máquinas virtuales de Azure, método hello qué Hola archivos binarios de aplicación se instalan en hello Máquina Virtual debe tener en cuenta. En este documento se explica cómo automatizar la instalación de aplicaciones mediante extensiones de script personalizadas para máquinas virtuales de Azure.

objetivo de Hello al desarrollar plantillas del Administrador de recursos de Azure es tooautomate implementación de saludo de la infraestructura de Azure e instalación de Hola y la configuración de las aplicaciones hospedadas en esta infraestructura de Azure. En estos artículos se proporciona un ejemplo de esta experiencia.

## <a name="deploy-hello-music-store-application"></a>Implementar la aplicación hello de la tienda de música
Hola aplicación de tienda de música puede implementarse mediante este botón.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-windows%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/>
</a>

plantilla de Azure Resource Manager Hola requiere Hola después de los valores de parámetro.

| Nombre de parámetro | Descripción |
| --- | --- |
| ADMINUSERNAME |Nombre de usuario de administrador que se usa en la máquina virtual de Hola y Hola base de datos de SQL Azure. |
| ADMINPASSWORD |Contraseña que se usa en la máquina Virtual de Azure de Hola y de base de datos SQL. |
| NUMBEROFINSTANCES |número de Hola de toobe de máquinas virtuales que se creó. Cada una de estas aplicaciones web de máquinas virtuales host Hola tienda de música y todo el tráfico tiene una carga equilibrada entre ellos. |
| PUBLICIPADDRESSDNSNAME |Nombre DNS único global había asociado Hola dirección IP pública. |

Cuando haya finalizado la implementación de la plantilla de hello, busque toohello dirección de IP pública mediante cualquier explorador de internet. Hola .net se presentará el sitio de música de núcleo.

## <a name="next-steps"></a>Pasos siguientes
<hr>

[Paso 1: arquitectura de aplicaciones con plantillas de Azure Resource Manager](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Paso 2: acceso y seguridad en plantillas de Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Paso 3: disponibilidad y escala en plantillas de Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Paso 4: implementación de aplicaciones con plantillas de Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

