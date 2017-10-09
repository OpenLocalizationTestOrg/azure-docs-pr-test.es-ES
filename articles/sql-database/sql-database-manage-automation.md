---
title: "aaaManage bases de datos de SQL de Azure mediante automatización de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se Hola servicio automatización de Azure pueden toomanage usa las bases de datos SQL de Azure a escala."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Administración de bases de datos SQL de Azure mediante Automatización de Azure
Esta guía le presentará los toohello servicio de automatización de Azure y cómo puede resultarle toosimplify usa la administración de las bases de datos de SQL Azure.

## <a name="what-is-azure-automation"></a>¿Qué es Automatización de Azure?
[Automatización de Azure](https://azure.microsoft.com/services/automation/) es un servicio de Azure para simplificar la administración en la nube mediante la automatización de procesos. Mediante automatización de Azure, las tareas de ejecución prolongada, manuales, propensa a errores y repiten con frecuencia pueden ser tooincrease automatizadas confiabilidad y eficacia, toovalue de tiempo para su organización.

Automatización de Azure ofrece un motor de ejecución de flujo de trabajo altamente confiable y alta disponibilidad que escala toomeet sus necesidades a medida que crece la organización. En Automatización de Azure, los sistemas de terceros pueden interrumpir los procesos manualmente o en intervalos programados para que las tareas se realicen justo cuando sea necesario.

Reducir la sobrecarga operativa y liberar TI / DevOps toofocus de personal en el trabajo que agrega valor empresarial moviendo el toobe de tareas de administración en la nube se ejecute automáticamente mediante la automatización de Azure.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>¿Cómo puede Automatización de Azure ayudar a administrar bases de datos SQL de Azure?
La base de datos de SQL Azure pueden administrarse en automatización de Azure mediante el uso de hello [cmdlets de PowerShell de base de datos de SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) que están disponibles en hello [herramientas de Azure PowerShell](/powershell/azure/overview). Automatización de Azure tiene estos cmdlets de PowerShell de base de datos de SQL Azure disponibles fuera del cuadro de hello, por lo que puede realizar todas las tareas de administración de base de datos SQL en el servicio de Hola. También se puede emparejar estos cmdlets en automatización de Azure con los cmdlets de Hola para otros servicios de Azure, tareas complejas tooautomate a través de los servicios de Azure y sistemas de terceros 3rd.

Automatización de Azure tiene también Hola capacidad toocommunicate con servidores SQL Server directamente, mediante la emisión de comandos SQL con PowerShell.

Hola [Galería de runbooks de automatización de Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene una variedad de producto equipo y la Comunidad runbooks tooget iniciado automatizar la administración de bases de datos de SQL Azure, otros servicios de Azure y sistemas de terceros 3rd. Los runbooks de la Galería incluyen:

* [Ejecución de consultas SQL en una Base de datos de SQL Server](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [Escalación vertical (arriba o abajo) de una Base de datos SQL de Azure en una programación](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Truncamiento de una tabla SQL si su base de datos se aproxima al tamaño máximo](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Indexación de tablas en una Base de datos SQL de Azure si están muy fragmentadas](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de automatización de Azure y cómo puede resultarle toomanage usado bases de datos de SQL Azure, siga estas toolearn de vínculos más información acerca de la automatización de Azure.

* [Información general sobre Automatización de Azure](../automation/automation-intro.md)
* [Mi primer runbook](../automation/automation-first-runbook-graphical.md)
* [Mapa de aprendizaje de Automatización de Azure](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Automatización de Azure: El agente de SQL en hello en la nube](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

