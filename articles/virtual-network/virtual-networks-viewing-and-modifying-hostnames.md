---
title: aaaViewing y modificar los nombres de host | Documentos de Microsoft
description: "Cómo tooview y cambie nombres de host de máquinas virtuales de Azure, web y roles de trabajo para la resolución de nombres"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Ver y modificar los nombres de host
tooallow su toobe de instancias de rol al que hace referencia el nombre de host, debe establecer valor de hello para el nombre de host de hello en el archivo de configuración de servicio de Hola para cada rol. Hacerlo agregando toohello de nombre de host de hello deseado **vmName** atributo de hello **rol** elemento. Hola valo hello **vmName** atributo se usa como base para el nombre de host de Hola de cada instancia de rol. Por ejemplo, si **vmName** es *webrole* y hay tres instancias de ese rol, nombres de host de Hola de instancias de hello será *webrole0*, *webrole1* , y *webrole2*. No es necesario toospecify un nombre de host para máquinas virtuales en el archivo de configuración de hello, porque el nombre de host de Hola para una máquina virtual se rellena según el nombre de equipo virtual Hola. Para obtener más información sobre cómo configurar un servicio de Microsoft Azure, consulte [Esquema de configuración del servicio de Azure (archivo de .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>Ver nombres de host
Puede ver los nombres de host de Hola de máquinas virtuales e instancias de rol en un servicio de nube mediante cualquiera de las herramientas de Hola a continuación.

### <a name="azure-portal"></a>Portal de Azure
Puede usar hello [portal de Azure](http://portal.azure.com) tooview nombres de host de Hola para máquinas virtuales en la hoja de información general de Hola para una máquina virtual. Tenga en cuenta que Hola hoja muestra un valor de **nombre** y **nombre de Host**. Aunque inicialmente son Hola iguales, cambiar el nombre de host de hello no cambiará nombre Hola de máquina virtual de Hola o instancia de rol.

Instancias de rol también pueden verse en hello portal de Azure, pero cuando se enumeran las instancias de hello en un servicio de nube, no se muestra el nombre de host de Hola. Verá un nombre para cada instancia, pero ese nombre no representa el nombre de host de Hola.

### <a name="service-configuration-file"></a>Archivo de configuración de servicio
Puede descargar el archivo de configuración de servicio de Hola para un servicio implementado de hello **configurar** hoja del servicio de Hola Hola portal de Azure. A continuación, busque Hola **vmName** atributo para hello **nombre de rol** nombre de host de elemento toosee Hola. Tenga en cuenta que este nombre de host se usa como base para el nombre de host de Hola de cada instancia de rol. Por ejemplo, si **vmName** es *webrole* y hay tres instancias de ese rol, nombres de host de Hola de instancias de hello será *webrole0*, *webrole1* , y *webrole2*.

### <a name="remote-desktop"></a>Escritorio remoto
Después de habilitar Escritorio remoto (Windows), comunicación remota de Windows PowerShell (Windows) o tooyour las conexiones SSH (Linux y Windows) máquinas virtuales o instancias de rol, puede ver el nombre de host de Hola desde una conexión activa de escritorio remoto de varias maneras:

* Escriba el nombre de host en el símbolo del sistema de Hola o terminal de SSH.
* Escriba ipconfig/todo en comando hello, símbolo del sistema (solo Windows).
* Nombre del equipo de Hola de vista en el sistema de Hola configuración (solo Windows).

### <a name="azure-service-management-rest-api"></a>API de REST de Administración de servicios de Azure
Desde un cliente REST, siga estas instrucciones:

1. Asegúrese de que tiene un toohello de tooconnect de certificado de cliente portal de Azure. tooobtain un certificado de cliente, siga los pasos de hello presentados en [Cómo: descargar y configuración de publicación de importación y la información de suscripción](https://msdn.microsoft.com/library/dn385850.aspx). 
2. Establezca una entrada de encabezado denominada x-ms-version con un valor de 2013-11-01.
3. Enviar una solicitud de hello siguiendo el formato: https://management.core.windows.net/\<identificador de opción\>/services/hostedservices/\<nombre del servicio\>? detalle incrustar = true
4. Busque hello **HostName** para cada elemento **RoleInstance** elemento.

> [!WARNING]
> También puede ver sufijo de dominio interno de hello para el servicio de respuesta a llamadas REST de hello en la nube mediante la comprobación de hello **InternalDnsSuffix** elemento, o mediante la ejecución de ipconfig/todo ello desde un símbolo del sistema en una sesión de escritorio remoto (Windows) o bien por ejecución /etc/resolv.conf cat desde un terminal SSH (Linux).
> 
> 

## <a name="modifying-a-hostname"></a>Modificar un nombre de host
Puede modificar el nombre de host de Hola para cualquier máquina virtual o instancia de rol mediante la carga de un archivo de configuración de servicio modificado, o cambiar el nombre de equipo de Hola desde una sesión de escritorio remoto.

## <a name="next-steps"></a>Pasos siguientes
[resolución de nombres DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Esquema de configuración del servicio de Azure (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Esquema de configuración de red virtual de Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Especificación de la configuración de DNS usando los archivos de configuración de red](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

