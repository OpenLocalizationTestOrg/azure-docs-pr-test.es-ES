---
title: "actualización de la aplicación Fabric aaaService | Documentos de Microsoft"
description: "Este artículo proporciona una introducción tooupgrading una aplicación de Service Fabric, incluidos los modos de actualización elige la opción y realizar comprobaciones de mantenimiento."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>Actualización de la aplicación de Service Fabric
Una aplicación de Azure Service Fabric es una colección de servicios. Durante una actualización, Service Fabric compara Hola nueva [manifiesto de aplicación](service-fabric-application-model.md#describe-an-application) con la versión anterior de Hola y determina qué servicios en la aplicación hello requieren actualizaciones. Service Fabric compara versión Hola números en el servicio de hello manifiestos con números de versión de hello en la versión anterior de Hola. Si un servicio no ha cambiado, no se actualiza.

## <a name="rolling-upgrades-overview"></a>Información general de las actualizaciones graduales
En una actualización gradual de la aplicación, se realiza la actualización de Hola en fases. En cada fase, actualización de hello es tooa aplicado subconjunto de nodos de clúster de hello, llamada a un dominio de actualización. Como resultado, la aplicación hello sigue estando disponible a lo largo de la actualización de Hola. Durante la actualización de hello, clúster de hello puede contener una combinación de versiones de hello antiguos y nuevos.

Por esta razón, deben ser versiones Hola dos hacia delante y hacia atrás compatible. Si no son compatibles, Administrador de la aplicación hello es responsable de la disponibilidad de un toomaintain de actualización de varias fases de almacenamiento provisional. En una actualización de varias fases, primer paso de hello está actualizando tooan versión intermedia de aplicación Hola que es compatible con la versión anterior de Hola. Hola segundo paso es versión final de tooupgrade Hola que interrumpe la compatibilidad con versiones anteriores a la actualización de hello, pero es compatible con la versión intermedia Hola.

Dominios de actualización se especifican en el manifiesto de clúster de hello al configurar el clúster de Hola. Los dominios de actualización no reciben actualizaciones en un orden concreto. Un dominio de actualización es una unidad lógica de implementación para una aplicación. Dominios de actualización permiten Hola servicios tooremain a alta disponibilidad durante una actualización.

Las actualizaciones sucesivas no son posibles si la actualización de Hola se aplica tooall nodos en clúster de hello, que es el caso de hello cuando aplicación hello tiene solo un dominio de actualización. No se recomienda este enfoque, ya que el servicio Hola deja de funcionar y no está disponible en tiempo de presentación de la actualización. Además, Azure no ofrece ninguna garantía cuando se configura un clúster con un solo dominio de actualización.

## <a name="health-checks-during-upgrades"></a>Comprobaciones de estado durante las actualizaciones
Para realizar una actualización, las directivas de mantenimiento tienen toobe establecido (o se pueden utilizar los valores predeterminados). Una actualización se denomina correcta cuando haya actualizado todos los dominios de actualización dentro de hello especifica los tiempos de espera y, cuando actualización todos los dominios se consideran correcto.  Un dominio de actualización correcto significa que ese dominio de actualización de hello pasado todas las comprobaciones de mantenimiento de hello especificadas en la directiva de mantenimiento de Hola. Por ejemplo, una directiva de mantenimiento puede exigir que todos los servicios dentro de una instancia de la aplicación tienen que ser *correctos*, tal como Service Fabric define el estado correcto.

Las directivas de mantenimiento y comprobaciones de estado durante la actualización de Service Fabric son independientes de los servicios y aplicaciones. Es decir, no se realiza ninguna prueba específica del servicio.  Por ejemplo, el servicio puede tener un requisito de rendimiento, pero Service Fabric no tiene el rendimiento de la información toocheck Hola. Consulte toohello [artículos de mantenimiento](service-fabric-health-introduction.md) para las comprobaciones de Hola que se llevan a cabo. comprobaciones de Hola que se producen durante las pruebas de una actualización se incluyen para si el paquete de aplicación Hola se copió correctamente, si ha iniciado la instancia de hello y así sucesivamente.

estado de la aplicación Hello es una agregación de las entidades secundarias de Hola de aplicación hello. En resumen, Service Fabric evalúa mantenimiento Hola de aplicación Hola a través de mantenimiento de Hola que se notifica en la aplicación hello. También evalúa Hola estado de todos los servicios de hello para la aplicación hello así. Service Fabric más evalúa mantenimiento Hola Hola de servicios de aplicaciones al agregar el estado de Hola de sus elementos secundarios, como réplicas del servicio de Hola. Una vez que se cumple la directiva de mantenimiento de aplicación Hola, actualización de hello puede continuar. Si se infringe la directiva de mantenimiento de hello, se produce un error en la actualización de la aplicación hello.

## <a name="upgrade-modes"></a>Modos de actualización
Hola modo que se recomienda para la actualización de la aplicación es Hola supervisado, que es el modo de Hola de uso frecuente. Modo supervisado realiza una actualización de hello en el dominio de una actualización, y si comprueba el estado de todos los paso (por hello directiva especificada), se mueve en toohello siguiente dominio de actualización automáticamente.  Si hay producirá un error en las comprobaciones de mantenimiento o se alcanzan los tiempos de espera, Hola actualización está bien revertido para dominio de actualización de Hola o modo de hello toounmonitored modificados manual. Puede configurar hello toochoose actualización uno de los dos modos para errores de actualización. 

Modo manual no supervisado necesita intervención manual después de cada actualización en un dominio de actualización, tookick desactivar actualización hello en hello siguiente dominio de actualización. No se realiza ninguna comprobación de mantenimiento de Service Fabric. Administrador de Hello realiza comprobaciones de estado o de hello antes de iniciar la actualización de hello en hello siguiente dominio de actualización.

## <a name="upgrade-default-services"></a>Actualización de servicios predeterminados
Servicios predeterminados dentro de la aplicación de Service Fabric se pueden actualizar durante el proceso de actualización de Hola de una aplicación. Servicios predeterminados se definen en hello [manifiesto de aplicación](service-fabric-application-model.md#describe-an-application). Hola reglas estándar de la actualización de servicios predeterminados son:

1. Servicios en hello nueva predeterminados [manifiesto de aplicación](service-fabric-application-model.md#describe-an-application) que no existen en el clúster de Hola se crean.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) necesita toobe establecer tootrue tooenable Hola siguiendo las reglas. Esta característica se admite desde la versión 5.5.

2. Se actualizan los servicios predeterminados existentes del [manifiesto de aplicación](service-fabric-application-model.md#describe-an-application) anterior y los de la nueva versión. Descripciones de los servicios en la nueva versión de hello reemplazaría las que ya está en clúster de Hola. La actualización de aplicaciones se revertiría automáticamente tras el error de actualización de servicios.
3. Servicios en hello anterior predeterminados [manifiesto de aplicación](service-fabric-application-model.md#describe-an-application) pero no en la nueva versión de Hola se elimina. **Tenga en cuenta que no se pueden revertir esta eliminación de servicios predeterminados.**

En el caso de una aplicación se revierte la actualización, servicios predeterminados son toohello revertida estado antes de inicia la actualización. No obstante, nunca se pueden crear servicios eliminados.

## <a name="application-upgrade-flowchart"></a>Diagrama de flujo de actualización de la aplicación
diagrama de flujo de Hello siguiendo este párrafo puede ayudarle a entender el proceso de actualización de Hola de una aplicación de Service Fabric. En concreto, se describe el flujo de Hola Hola cómo los tiempos de espera, incluidos los *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, y *UpgradeHealthCheckInterval*, ayudar a controlar cuando se considera actualización hello en el dominio de una actualización correcta o un error.

![proceso de actualización de Hola para una aplicación de servicio de Fabric][image]

## <a name="next-steps"></a>Pasos siguientes
[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.

[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.

Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).

Hacer que las actualizaciones de la aplicación sea compatible por el aprendizaje cómo toouse [serialización de datos](service-fabric-application-upgrade-data-serialization.md).

Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).

Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
