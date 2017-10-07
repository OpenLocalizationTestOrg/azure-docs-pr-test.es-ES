---
title: "aaaManage almacén de claves de Azure mediante automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se Hola servicio automatización de Azure pueden toomanage usa el almacén de claves de Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Administración del Almacén de claves de Azure mediante Automatización de Azure
Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa administración de sus claves y secretos en el almacén de claves de Azure.

## <a name="what-is-azure-automation"></a>¿Qué es Automatización de Azure?
[Automatización de Azure](../automation/automation-intro.md) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos y la configuración de estado deseado. Mediante automatización de Azure, pueden ser, repetidas, larga ejecución, tareas manuales y propensas a errores tooincrease automatizadas confiabilidad y eficacia, toovalue de tiempo para su organización.

Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y de alta disponibilidad que escala toomeet sus necesidades. En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.

Reducir la sobrecarga operativa y liberar TI y DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>¿Cómo puede ayudar Automatización de Azure a administrar el Almacén de claves de Azure?
El almacén de claves se pueden administrar en automatización de Azure mediante hello [cmdlets del almacén de claves de AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) y [cmdlets del almacén de claves de Azure clásico](https://msdn.microsoft.com/library/azure/dn868052.aspx). Hola módulo de Azure para administrar el almacén de claves clásico está disponible automáticamente en automatización de Azure y se puede importar hello [AzureRM KeyVault módulo](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) en automatización de Azure, por lo que puede realizar muchas de la administración de almacén de claves tareas de servicio de Hola. También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros 3rd.

Con los cmdlets del almacén de claves de Azure Hola puede realizar estas tareas, entre otros: 

* Crear y configurar un almacén de claves
* Crear o importar una clave
* Crear o actualizar un secreto
* Actualizar los atributos de una clave
* Obtener una clave o un secreto
* Eliminar una clave o un secreto

Estos son algunos ejemplos del uso de PowerShell toomanage el almacén de claves:  

* [Azure Key Vault - Step by Step (Almacén de claves de Azure: paso a paso)](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Setting Up and Configuring an Azure Key Vault (Instalar y configurar un Almacén de claves de Azure)](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de automatización de Azure y cómo puede resultarle toomanage usa el almacén de claves de Azure, siga estas toolearn de vínculos más información acerca de la automatización de Azure.

* Vea Hola automatización de Azure [Tutorial de introducción](../automation/automation-first-runbook-graphical.md).
* Vea hello [scripts de PowerShell de almacén de claves de Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

