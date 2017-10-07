---
title: "tooAzure de problemas de conexión comunes de aaaTroubleshoot base de datos SQL"
description: "Pasos tooidentify y resolver comunes errores de conexión de base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Solucionar problemas de conexión tooAzure base de datos SQL
Cuando se produce un error en la conexión de hello tooAzure base de datos de SQL, recibirá [mensajes de error](sql-database-develop-error-messages.md). Este artículo es un tema centralizado que ayuda a la solución de problemas de conectividad de Base de datos SQL de Azure. Introduce [Hola causas comunes](#cause) de problemas de conexión, se recomienda [una herramienta de solución de problemas](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) que le ayuda a un problema de Hola de identidad y proporciona la solución de problemas de pasos toosolve [ los errores transitorios](#troubleshoot-transient-errors) y [persistentes o no transitorio errores](#troubleshoot-persistent-errors). 

Si encuentra problemas de conexión de hello, intente Hola solucionar problemas de los pasos que se describen en este artículo.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Causa
Problemas de conexión pueden deberse a alguna de hello siguientes:

* Error tooapply mejores prácticas y directrices de diseño durante el proceso de diseño de aplicación Hola.  Vea [información general sobre el desarrollo de base de datos de SQL](sql-database-develop-overview.md) tooget iniciado.
* Reconfiguración de la Base de datos SQL de Azure
* Configuración de firewall
* Tiempo de espera de conexión agotado
* Información de inicio de sesión incorrecta
* Límite máximo alcanzado en algunos recursos de Base de datos SQL de Azure

Por lo general, tooAzure de problemas de conexión base de datos SQL se puede clasificar como sigue:

* [Errores transitorios (corta duración o intermitentes)](#troubleshoot-transient-errors)
* [Errores persistentes o no transitorios (errores que se repiten con frecuencia)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Pruebe Hola Solucionador de problemas para los problemas de conectividad de base de datos de SQL Azure
Si se produce un error de conexión específico, pruebe [esta herramienta](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), que le ayudará a identificar y resolver el problema.

## <a name="troubleshoot-transient-errors"></a>Solución de problemas de errores transitorios

Cuando una aplicación conecta a base de datos de SQL Azure tooan, recibirá Hola mensaje de error siguiente:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Este mensaje de error suele ser transitorio (breve).
> 
> 

Este error se produce cuando hello Azure base de datos se va a mover (o volver a configurar) y la aplicación pierde su base de datos SQL de toohello de conexión. Los eventos de reconfiguración de la base de datos SQL se producen debido a un evento planeado (por ejemplo, una actualización de software) o a un evento no planeado (por ejemplo, el bloqueo de un proceso o un equilibrio de carga). La mayoría de los eventos de reconfiguración son generalmente de corta duración y se completarán en menos de 60 segundos. Sin embargo, estos eventos en ocasiones pueden tardar más tiempo toofinish, por ejemplo, cuando una transacción de grande provoca una recuperación de larga duración.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Problemas de conectividad temporal tooresolve de pasos

1. Comprobar hello [panel de servicios de Microsoft Azure](https://azure.microsoft.com/status) para los que las interrupciones conocidas que se produjeron durante el tiempo de Hola durante qué Hola haya notificado errores aplicación hello.
2. Las aplicaciones que se conectan tooa servicio en la nube como base de datos de SQL Azure debe esperar eventos periódicos volver a configurar e implementar Reintentar lógica toohandle estos errores en lugar de así como la exposición como toousers de errores de aplicación. Hola de revisión [errores transitorios](sql-database-connectivity-issues.md) hello y sección prácticas recomendadas y directrices en de diseño [información general sobre el desarrollo de base de datos de SQL](sql-database-develop-overview.md) para obtener más información y general de las estrategias de reintento. Después, para información específica, consulte ejemplos de código en [Bibliotecas de conexiones para Base de datos SQL y SQL Server](sql-database-libraries.md) .
3. Como una base de datos acerca a su límite de recursos, que puede parecer toobe un problema de conectividad temporal. Vea [Solucionar problemas de rendimiento](sql-database-troubleshoot-performance.md).
4. Si continúan los problemas de conectividad o si hello duración para la que la aplicación encuentra errores de hello supera los 60 segundos o si observa varias repeticiones del error de hello en un día determinado, una solicitud de soporte técnico de Azure de archivos seleccionando **obtener admite** en hello [soporte técnico de Azure](https://azure.microsoft.com/support/options) sitio.

## <a name="troubleshoot-persistent-errors"></a>Solución de problemas de los errores persistentes
Si aplicación hello no persistente tooconnect tooAzure base de datos SQL, suele indicar un problema con uno de hello siguientes:

* Configuración del firewall. firewall de base de datos o de cliente de SQL Azure Hola está bloqueando las conexiones tooAzure base de datos SQL.
* Volver a configurar en el lado del cliente de Hola de red: por ejemplo, una nueva dirección IP o un servidor proxy.
* Error de usuario: por ejemplo, esté escrita incorrectamente los parámetros de conexión, como nombre del servidor hello en la cadena de conexión de Hola.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Problemas de conectividad persistente de tooresolve de pasos
1. Configurar [las reglas de firewall](sql-database-configure-firewall-settings.md) dirección IP del cliente de tooallow Hola. Para temporal con fines de prueba, configure una regla de firewall mediante 0.0.0.0 como Hola a partir de intervalo de direcciones IP y 255.255.255.255 como Hola final del intervalo de direcciones IP. Se abrirá hello tooall direcciones IP. Si se resuelve el problema de conectividad, quite esta regla y cree una regla de firewall para una dirección IP o intervalo de direcciones apropiadamente limitados. 
2. En todos los firewalls entre el cliente de Hola y Hola Internet, asegúrese de que el puerto 1433 está abierto para las conexiones salientes. Revisión [configurar Firewall de Windows de hello tooAllow acceso a SQL Server](https://msdn.microsoft.com/library/cc646023.aspx) y [híbrida identidad requiere puertos y protocolos](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) para punteros adicionales relacionados con tooadditional puertos que necesita tooopen para Autenticación de Azure Active Directory.
3. Compruebe la cadena de conexión y otras opciones de conexión. Consulte la sección de la cadena de conexión en Hola Hola [tema de problemas de conectividad](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Compruebe el estado del servicio en el panel de Hola. Si cree que existe una interrupción regional, consulte [recuperarse de una interrupción](sql-database-disaster-recovery.md) de toorecover tooa nueva área de pasos.

## <a name="next-steps"></a>Pasos siguientes
* [Evaluación y mejora del rendimiento de la base de datos con la Base de datos SQL de Azure](sql-database-troubleshoot-performance.md)
* [Documentación de Hola de búsqueda en Microsoft Azure](http://azure.microsoft.com/search/documentation/)
* [Hola vista actualizaciones más recientes toohello servicio de base de datos de SQL Azure](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Recursos adicionales
* [Información general de desarrollo de Base de datos SQL](sql-database-develop-overview.md)
* [Orientación general sobre reintentos](../best-practices-retry-general.md)
* [Bibliotecas de conexiones para Base de datos SQL y SQL Server](sql-database-libraries.md)

