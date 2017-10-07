---
title: "aaaAzure diagnósticos y supervisión del servicio tejido contenedores | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor y diagnosticar los contenedores que se organiza en Microsoft Azure Service Fabric con soluciones de contenedores de OMS."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>Supervisión de contenedores de Windows Server con OMS

## <a name="oms-containers-solution"></a>Solución Containers de OMS

equipo de Operations Management Suite (OMS) Hola ha publicado una solución de contenedores para diagnósticos y supervisión para los contenedores. Junto con su solución de Service Fabric, esta solución es un implementaciones de contenedor de toomonitor herramienta excelente organiza en el tejido de servicio. Este es un ejemplo sencillo de qué panel hello en soluciones de hello es similar:

![Panel de OMS básico](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

También recopila diferentes tipos de registros que se pueden consultar en la herramienta de análisis de registros de OMS de hello, y puede ser usado toovisualize cualquier métricas o eventos que se está generados. los tipos de registro de Hello que se recopilan son:

1. ContainerInventory: muestra información acerca de la ubicación, nombre e imágenes del contenedor
2. ContainerImageInventory: información acerca de las imágenes implementadas, lo que incluye sus identificadores o tamaños
3. ContainerLog: registros de error concretos, registros de docker (stdout, etc.) y otras entradas
4. ContainerServiceLog: comandos de demonio de docker que se han ejecutado
5. Rendimiento: contadores de rendimiento incluido contenedor cpu, memoria, tráfico de red, la e/s de disco y métricas personalizadas de hello hospedan máquinas

Este artículo tratan Hola pasos necesarios tooset la supervisión para el clúster de contenedor. más información acerca de la solución de contenedores de OMS, toolearn desproteger sus [documentación](../log-analytics/log-analytics-containers.md).

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Configuración de un clúster de Service Fabric

Crear un clúster con la plantilla de Azure Resource Manager Hola encuentra [aquí](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample). Asegúrese de que tooadd un único nombre de área de trabajo OMS. Esta plantilla también tiene como valor predeterminado de toodeploying crear un clúster en la vista previa de Hola de Service Fabric (v255.255), lo que significa que no se puede usar en producción y no se puede actualiza tooa otra versión de Service Fabric. Si decide toouse esta plantilla para a largo plazo o de producción usan, cambiar el número de versión estable de hello versión tooa.

Una vez configurado el clúster de hello, confirme que ha instalado el certificado adecuado de Hola y asegúrese de que es capaz de tooconnect toohello clúster.

Confirme que el grupo de recursos se ha configurado correctamente por título toohello [portal de Azure](https://portal.azure.com/) y buscar la implementación de Hola. grupo de recursos de Hello debería contener todos los recursos de Service Fabric hello y, también tiene una solución de análisis de registros, así como una solución de Service Fabric.

Para modificar un clúster de Service Fabric existente:
* Confirme que esté habilitado diagnósticos (si no es así, habilitarla a través de [actualizar conjunto de escalas de máquina virtual de hello](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* Agregar un área de trabajo de OMS mediante la creación de una solución de "Análisis de tejido de servicio" a través de hello Azure Marketplace
* Editar orígenes de datos de Hola de hello Service Fabric solución toopick datos en tablas de almacenamiento de Azure adecuadas de hello (configurar wad) Hola grupo de recursos que Hola clúster está en
* Agregar agente de Hola como un [conjunto de escalas de máquina virtual de extensión toohello](/powershell/module/azurerm.compute/add-azurermvmssextension) a través de PowerShell o a través de actualizar el conjunto de escalas de máquina virtual de hello (mismo vínculo anterior, plantilla de administrador de recursos de hello toomodify)

## <a name="2-deploy-a-container"></a>2. Implementación de un contenedor

Una vez que el clúster Hola está listo y haber confirmado que puede acceder a ella, implemente un tooit del contenedor. Si elige versión de vista previa de hello toouse como conjunto por plantilla de hello, también puede explorar docker nueva de Service Fabric crean la funcionalidad. Tenga en cuenta que Hola primera vez una imagen de contenedor es tooa implementado clúster, se aplican varias imágenes de hello toodownload de minutos dependiendo de su tamaño.

## <a name="3-add-hello-containers-solution"></a>3. Agregar la solución de contenedores de Hola

En el portal de Azure de Hola, cree un recurso de contenedores (bajo Hola supervisión + administración categoría) a través de Azure Marketplace. 

![Adición de la solución Containers](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

En el paso de creación de hello, solicita un área de trabajo OMS. Seleccione Hola uno que se creó con la implementación de hello anterior. Este paso agrega una solución de contenedores en el área de trabajo OMS y se detecta automáticamente por el agente OMS Hola implementado por plantilla de Hola. agente de Hello empezará a recopilar datos en procesos de contenedores de hello en clúster de Hola y en aproximadamente 10-15 minutos, debería ver soluciones Hola claro seguridad con datos como en la imagen de hello del panel de hello anterior de.

## <a name="4-next-steps"></a>4. Pasos siguientes

OMS ofrece diversas herramientas de hello toomake de área de trabajo si es más útil para usted. Explorar Hola después opciones toocustomize Hola solución tooyour necesidades:
- Obtener las nociones básicas de hello [Iniciar búsqueda y la consulta](../log-analytics/log-analytics-log-searches.md) que ofrece características como parte del análisis de registros
- Configurar toopick de agente OMS Hola los contadores de rendimiento específicos (ir toohello área de trabajo principal > Configuración > datos > contadores de rendimiento de Windows)
- Configurar OMS tooset [automatizada alertas](../log-analytics/log-analytics-alerts.md) tooaid de reglas en la detección y diagnóstico
