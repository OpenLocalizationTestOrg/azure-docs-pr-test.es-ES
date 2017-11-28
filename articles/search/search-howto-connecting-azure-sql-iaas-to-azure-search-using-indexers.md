---
title: "tooAzure de conexión de máquina virtual de aaaSQL búsqueda | Documentos de Microsoft"
description: "Habilitar conexiones cifradas y configure Hola firewall tooallow conexiones tooSQL Server en una máquina virtual Azure (VM) de un indizador de búsqueda de Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Configurar una conexión desde un tooSQL de indizador de búsqueda de Azure Server en una máquina virtual de Azure
Como se indicó en [tooAzure de conexión de base de datos de SQL de Azure Buscar utilizar indizadores](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), creación de indizadores en **SQL Server en máquinas virtuales de Azure** (o **máquinas virtuales de Azure SQL** abreviado) es compatible con la búsqueda de Azure, pero hay algunos tootake de requisitos previos relacionados con la seguridad atención primero. 

**Duración de la tarea:** unos 30 minutos, suponiendo que ya instaló un certificado en hello máquina virtual.

## <a name="enable-encrypted-connections"></a>Habilitación de conexiones cifradas
Azure Search requiere un canal cifrado para todas las solicitudes del indexador a través una conexión pública a Internet. Esta sección enumeran Hola pasos toomake este trabajo.

1. Comprobar propiedades de hello del nombre de sujeto de hello certificado tooverify Hola es el nombre de dominio completo (FQDN) de Hola de hello VM de Azure. Puede utilizar una herramienta como CertUtils u Hola certificados complemento tooview Hola propiedades. Puede obtener Hola FQDN de sección de Essentials de hoja del servicio VM hello, Hola **IP pública dirección/nombre de DNS etiqueta** campo, hello [portal de Azure](https://portal.azure.com/).
   
   * Para las máquinas virtuales creadas con versiones más recientes de hello **el Administrador de recursos** plantilla, se da formato Hola FQDN como `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Para máquinas virtuales anteriores que se crea como un **clásico** VM, hello tiene el formato FQDN `<your-cloud-service-name.cloudapp.net>`. 
2. Configurar SQL Server toouse hello mediante Hola Editor del registro (regedit). 
   
    Aunque el Administrador de configuración de SQL Server se usa a menudo para esta tarea, no se puede utilizar para este escenario. Si no encuentra Hola importa certificado porque Hola FQDN de hello VM en Azure no coincide con hello FQDN según lo determinado por hello VM (identifica dominio hello como equipo local de Hola o toowhich de dominio de red de Hola que se ha unido). Cuando no coinciden los nombres, usar certificado de regedit toospecify Hola.
   
   * En regedit, busque la clave del registro de toothis: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Hola `[MSSQL13.MSSQLSERVER]` parte varía en función de la versión y nombre de instancia. 
   * Establecer valor de Hola de hello **certificado** toohello clave **huella digital** del certificado SSL de hello importado toohello máquina virtual.
     
     Hay varias maneras tooget Hola huella digital algunas mejor que otros. Si copia desde hello **certificados** un complemento de MMC, probablemente seleccionará un carácter inicial invisible [tal y como se describe en este artículo de soporte técnico](https://support.microsoft.com/kb/2023869/), que da como resultado un error cuando intente una conexión. Existen varias soluciones para corregir este problema. Hola más fácil es toobackspace a lo largo y, a continuación, vuelva a escribir el primer carácter de Hola de hello huella digital tooremove Hola carácter inicial en el campo de valor de clave de hello en regedit. Como alternativa, puede usar una huella digital de otra herramienta toocopy Hola.
3. Conceder permisos de cuenta de servicio de toohello. 
   
    Asegúrese de que Hola cuenta de servicio de SQL Server se concede permiso adecuado en la clave privada de hello del certificado SSL de Hola. Si pasa por alto este paso, SQL Server no se iniciará. Puede usar hello **certificados** complemento o **CertUtils** para esta tarea.
4. Reinicie el servicio de SQL Server de Hola.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>Configurar la conectividad de SQL Server en hello VM
Después de configurar la conexión de hello cifrado requerida la búsqueda de Azure, hay una configuración adicional de pasos intrínseco tooSQL Server en máquinas virtuales de Azure. Si aún no lo ha no lo ha hecho, Hola próximo paso es configuración toofinish mediante uno de estos artículos:

* Para una **el Administrador de recursos** VM, consulte [conectar tooa Máquina Virtual de SQL Server en Azure mediante el Administrador de recursos](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* Para una **clásico** VM, consulte [conectar tooa Máquina Virtual de SQL Server en Azure clásico](../virtual-machines/windows/classic/sql-connect.md).

En particular, revise la sección de hello en cada artículo para "conectar a través de Hola internet".

## <a name="configure-hello-network-security-group-nsg"></a>Configurar Hola grupo de seguridad de red (NSG)
No es inusual tooconfigure Hola NSG y extremo correspondiente de Azure o lista de Control de acceso (ACL) toomake sus partes de tooother accesible de máquina virtual de Azure. Lo más probable es que ha realizado esto antes tooallow su propio tooyour tooconnect de lógica de aplicación VM de SQL Azure. Es similar para una tooyour de conexión de búsqueda de Azure VM de SQL Azure. 

Hola vínculos siguientes proporcionan instrucciones sobre la configuración de NSG para las implementaciones de máquina virtual. Siga estas instrucciones que tooacl un punto de conexión de la búsqueda de Azure en función de su dirección IP.

> [!NOTE]
> Para más información, consulte [¿Qué es un grupo de seguridad de red?](../virtual-network/virtual-networks-nsg.md)
> 
> 

* Para una **el Administrador de recursos** VM, consulte [cómo toocreate NSG para las implementaciones de ARM](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* Para una **clásico** VM, consulte [cómo toocreate NSG para las implementaciones de clásico](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

Asignación de direcciones IP puede suponer algunos de los desafíos que se solucionan fácilmente si es consciente del problema de Hola y soluciones alternativas posibles. en las secciones restantes Hola se proporcionan recomendaciones para tratar problemas relacionadas tooIP direcciones Hola ACL.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Restringir la dirección IP del servicio de búsqueda de toohello de acceso
Se recomienda encarecidamente que restrinja hello toohello IP dirección de acceso a su servicio de búsqueda de hello ACL en lugar de hacer que las máquinas virtuales de Azure de SQL muy abierta tooany las solicitudes de conexión. Puede encontrar fácilmente Hola IP dirección haciendo ping Hola FQDN (por ejemplo, `<your-search-service-name>.search.windows.net`) de su servicio de búsqueda.

#### <a name="managing-ip-address-fluctuations"></a>Administración de las fluctuaciones de dirección IP
Si el servicio de búsqueda tiene solo una unidad de búsqueda (es decir, una réplica y una partición), dirección IP de hello cambiará durante el reinicio de servicios de rutina, lo que invalida una ACL existente con la dirección IP del servicio de la búsqueda.

Error de conectividad posteriores hello tooavoid unidireccional es toouse más de una réplica y una partición en la búsqueda de Azure. Si lo hace, incrementa el costo de hello, pero también resuelve el problema de direcciones IP de Hola. En Azure Search, las direcciones IP no cambian cuando hay más de una unidad de búsqueda.

Un segundo enfoque es tooallow Hola conexión toofail y, a continuación, volver a configurar Hola ACL en hello NSG. En promedio, puede esperar toochange de direcciones IP cada pocas semanas. Para los clientes que realizan una indexación controlado muy de tarde en tarde, este enfoque puede ser viable.

Un tercer enfoque viable (pero no es particularmente seguro) es toospecify Hola intervalo de direcciones IP Hola región de Azure donde se aprovisione el servicio de búsqueda. lista de Hola de intervalos IP desde el que las direcciones IP públicas se asignan recursos tooAzure se publica en [intervalos de direcciones IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Incluir direcciones IP de portal de hello búsqueda de Azure
Si usas hello toocreate portal Azure un indizador, lógica de búsqueda de Azure de portal también necesita acceso tooyour SQL Azure VM durante la hora de creación. Las direcciones IP del portal de Azure Search se pueden encontrar haciendo ping en `stamp2.search.ext.azure.com`.

## <a name="next-steps"></a>Pasos siguientes
Con configuración fuera del modo de hello, ahora puede especificar un servidor SQL Server en la máquina virtual de Azure como origen de datos de Hola para un indizador de búsqueda de Azure. Vea [tooAzure de conexión de base de datos de SQL de Azure Buscar utilizar indizadores](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) para obtener más información.

