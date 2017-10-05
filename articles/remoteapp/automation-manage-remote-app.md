---
title: "Administración de Azure RemoteApp mediante Azure Automation | Microsoft Docs"
description: "Obtenga información acerca de cómo puede usarse el servicio Automatización de Azure para administrar RemoteApp de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a>Administración de RemoteApp de Azure mediante Automatización de Azure
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Esta guía le ofrece el servicio Automatización de Azure y cómo se puede usar para simplificar la administración de RemoteApp de Azure.

## <a name="what-is-azure-automation"></a>¿Qué es Automatización de Azure?
[Automatización de Azure](../automation/automation-intro.md) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos. Mediante Automatización de Azure, se pueden automatizar las tareas de ejecución prolongada, manuales, propensas a errores y que se repiten con frecuencia para aumentar la confiabilidad, la eficiencia y el valioso tiempo para su organización.

Automatización de Azure proporciona un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que realiza la escalación para satisfacer sus necesidades. En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.

Reduzca la sobrecarga operativa y libere al personal de TI/DevOps para concentrarse en el trabajo que proporciona valor al negocio trasladando las tareas de administración en la nube para que se ejecuten automáticamente mediante Automatización de Azure.

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a>¿Cómo puede ayudar el servicio Automatización de Azure a administrar RemoteApp de Azure?
RemoteApp se puede administrar en Automatización de Azure mediante los cmdlets de PowerShell que están disponibles en las [Herramientas de Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx). Automatización de Azure tiene estos cmdlets de PowerShell de RemoteApp disponibles directamente para que pueda realizar todas las tareas de administración de RemoteApp dentro del servicio. También puede emparejar estos cmdlets en Automatización de Azure con los cmdlets para otros servicios de Azure, para automatizar tareas complejas a través de los servicios de Azure y sistemas de terceros.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido los aspectos básicos de Automatización de Azure y cómo se puede usar para administrar RemoteApp de Azure, siga estos vínculos para obtener más información acerca de Automatización de Azure.

* Consulte el [Tutorial de introducción](../automation/automation-first-runbook-graphical.md)

