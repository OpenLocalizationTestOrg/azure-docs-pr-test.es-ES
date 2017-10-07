---
title: "información general de instancias de contenedor aaaAzure | Documentos de Azure"
description: "Descripción de Azure Container Instances"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a>Azure Container Instances

Los contenedores están convirtiéndose en toopackage de manera Hola preferido, implementar y administrar aplicaciones en la nube. Instancias de contenedor de Azure ofrece hello más rápido y toorun de forma más sencilla un contenedor en Azure, sin necesidad de tooprovision todas las máquinas virtuales y sin necesidad de tooadopt un servicio de nivel superior. 

Azure Container Instances es una excelente solución para cualquier escenario que pueda funcionar en contenedores aislados, incluidas las aplicaciones simples, la automatización de tareas y los trabajos de compilación. Para escenarios donde necesita completos orquestación de contenedor, incluida la detección de servicios en varios contenedores, el escalado automático y las actualizaciones de aplicaciones coordinadas, se recomienda hello [servicio de contenedor de Azure](https://docs.microsoft.com/azure/container-service/).

## <a name="fast-startup-times"></a>Tiempos de inicio rápido

Los contenedores ofrecen importantes ventajas de inicio sobre las máquinas virtuales. Con instancias de contenedor de Azure, puede iniciar un contenedor de Azure en segundos sin Hola necesidad tooprovision y administrar las máquinas virtuales.

## <a name="hypervisor-level-security"></a>Seguridad de nivel de hipervisor

Históricamente, los contenedores han ofrecido aislamiento a la dependencia entre aplicaciones y gobierno de recursos, pero no se han considerado suficientemente protegidos para el uso de varios inquilinos hostiles. Con Azure Container Instances, la aplicación está tan aislada en un contenedor como lo estaría en una máquina virtual.

## <a name="custom-sizes"></a>Tamaños personalizados

Los contenedores son normalmente optimizado toorun solo una única aplicación, sino necesidades exactas de Hola de esas aplicaciones pueden diferir considerablemente. Con Azure Container Instances, puede solicitar exactamente lo que necesita en relación a la memoria y núcleos de CPU. Se paga según lo que se solicita, facturado por hello segundo lugar, para que se pueden optimizar con precisión los gastos según sus necesidades.

## <a name="public-ip-connectivity"></a>Conectividad IP pública

Con instancias de contenedor de Azure, puede exponer los contenedores directamente toohello internet con una dirección IP pública. Hola futuras, se se expanda nuestra red capacidades tooinclude la integración con redes virtuales, carga equilibradores y otras partes principales de hello Azure infraestructura de red.

## <a name="persistent-storage"></a>Almacenamiento persistente

tooretrieve y conservar el estado con instancias de contenedor de Azure, le ofrecemos recursos compartidos de archivos de montaje directo de Azure.

## <a name="linux-and-windows-containers"></a>Contenedores de Linux y Windows

Con instancias de contenedor de Azure, puede programar ambas ventanas y contenedores de Linux con Hola misma API. Simplemente indican el tipo de sistema operativo base de Hola y todo lo demás es idéntica.

## <a name="co-scheduled-groups"></a>Grupos con programación compartida

Azure Container Instances admite la programación de grupos con varios contenedores que comparten una máquina host, la red local, el almacenamiento y el ciclo de vida. Esto permite toocombine la aplicación principal con otras personas que actúa en una función auxiliar, como el registro.

## <a name="next-steps"></a>Pasos siguientes

Intente implementar un tooAzure de contenedor con un único comando con nuestro [Guía de inicio rápido](container-instances-quickstart.md).
