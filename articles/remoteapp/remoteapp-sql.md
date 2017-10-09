---
title: aaaSQL Azure con Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse SQL Azure con Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>SQL Azure con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

A menudo, cuando los clientes eligen toohost sus aplicaciones de Windows en la nube de hello con Azure RemoteApp también desean toomigrate sus datos como los servidores SQL en hello en la nube para una implementación completa en la nube. Esto permite que cualquier dispositivo en cualquier lugar pueda acceder a la solución hospedada en la nube completa en cualquier momento con Azure RemoteApp. A continuación son vínculos y referencias junto con instrucciones toohelp usted con este proceso.  

## <a name="migrate-your-sql-data"></a>Migración de los datos SQL
Comience con [migrar un tooAzure de base de datos base de datos SQL de SQL Server](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Configuración de Azure RemoteApp
Hospede la aplicación de Windows en Azure RemoteApp. A continuación se muestran unas instrucciones paso a paso de un nivel muy alto:

1. Crear hello [plantilla de RemoteApp de Azure VM](remoteapp-imageoptions.md). 
2. Instalar aplicación hello necesario en hello máquina virtual.
3. Configure la aplicación hello por lo que se conecta toohello base de datos SQL y asegúrese de que funciona.
4. Hola de Sysprep y apague máquinas virtuales. Captúrelo como una imagen para usarlo con Azure. **Nota:** debe tooensure que aplicación hello es capaz de tooretain información de conectividad de Hola DB a través del proceso de sysprep de Hola. Si aplicación hello es información de conexión de no se puede tooretain Hola DB, puede ser conveniente tooengage proveedor de Hola de hello aplicación toocheck cómo podemos especificar cadena de conexión de Hola.
5. Importar imagen personalizada hello en la biblioteca de Azure RemoteApp selección de ubicación geográfica adecuada Hola que reside la implementación de SQL Azure. 
6. Implementar una colección de RemoteApp en hello mismo data center como la implementación de SQL Azure mediante Hola por encima de la plantilla y publica la aplicación hello. Implementar Azure RemoteApp en hello mismo centro de datos como la implementación de SQL Azure le ayuda a garantizar las velocidades de conexión más rápidas de Hola y reducir la latencia. 

## <a name="app-and-sql-configuration-considerations"></a>Consideraciones de configuración de RemoteApp y SQL:
Hay unos tooconsider puntos al usar SQL Azure con conexión de RemoteApp:

Obtenga información acerca de [cómo tooconfigure SQL Azure base de datos firewall](../sql-database/sql-database-firewall-configure.md). Un extracto de Estados de artículo hello, "inicialmente, servidor de base de datos SQL Azure de todos los acceso tooyour está bloqueado por hello firewall. En orden toobegin con el servidor de base de datos de SQL Azure, debe ir toohello Portal clásico y especificar una o varias reglas de firewall de nivel de servidor que habilitar el servidor de base de datos de SQL Azure tooyour de acceso. Use toospecify de reglas de firewall de hello dirección IP que va de hello Internet se permiten y si las aplicaciones de Azure pueden tratar de servidor de base de datos de SQL Azure tooyour tooconnect."

Además, cuando un equipo intenta tooconnect tooyour servidor de base de datos de Internet de hello, firewall de Hola comprueba Hola dirección IP de solicitud de hello en el conjunto completo de Hola de nivel de servidor de origen y (si es necesario) las reglas de firewall de nivel de base de datos. "Si dirección IP de saludo de solicitud de hello es dentro de uno de los intervalos de hello especificados en las reglas de firewall de nivel de servidor de hello, conexión Hola se concede tooyour servidor de base de datos de SQL Azure." Por lo tanto, podemos usar intervalos de direcciones IP, no solo direcciones IP de origen individuales.

Siga las instrucciones paso a paso de hello en [Cómo: configurar el firewall en la base de datos de SQL mediante hello Azure Portal](../sql-database/sql-database-configure-firewall-settings.md) intervalo IP toospecify Hola. Al configurar las reglas de Firewall de SQL de hello, proporcione intervalo IP de Hola de subred de Hola que se especifica para hello colección RemoteApp de Azure. Debe permitir a servidores de ARA hello tooconnect toohello base de datos SQL, aunque habrá-asignan dinámicamente direcciones IP.

## <a name="troubleshooting"></a>Solución de problemas
Si experimenta Hola del uso de una aplicación de cliente que se hospeda en Azure RemoteApp que se conecta tooa SQL de base de datos donde se hospeda en Azure o local es lento podría haber algunos motivos por qué.  

* Latencia de red de su dispositivo tooAzure es alta. Mueva la conexión de red mejor y más rápida de toohello para obtener el mejor rendimiento. Use [azurespeed.com](http://azurespeed.com/) como una herramienta general tootest centrar los datos de tooAzure de latencia de dispositivos.  
* La aplicación cliente hospedada en Azure RemoteApp está bajo presión. Seleccionar un plan de facturación diferente, como la facturación Premium, mejorará el rendimiento. Otro truco es recursos de hello toomonitor su aplicación está consumiendo: durante una sesión activa, realizar una secuencia de teclas ctrl-alt-end que se iniciará Hola SAS pantalla, seleccione el Administrador de tareas y observe la utilización de recursos para la aplicación.
* SQL Server está bajo presión o no está optimizado. Siga las instrucciones de SQL para la solucionar el problema. 

