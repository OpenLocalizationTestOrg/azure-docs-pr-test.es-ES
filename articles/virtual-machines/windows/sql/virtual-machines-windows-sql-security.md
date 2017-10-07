---
title: Consideraciones para SQL Server en Azure aaaSecurity | Documentos de Microsoft
description: "En este tema se proporcionan instrucciones generales para proteger SQL Server en ejecución en una máquina virtual de Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Consideraciones de seguridad para SQL Server en Máquinas virtuales de Azure

Este tema incluye instrucciones completas de seguridad que ayudan a establecer instancias del servidor de acceso seguro tooSQL en una máquina virtual (VM) de Azure.

Azure es compatible con varias de las normativas del sector y estándares que le permiten toobuild una solución compatible con SQL Server en una máquina virtual. Para obtener información acerca del cumplimiento normativo de Azure, consulte [Centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Controlar el acceso toohello VM de SQL

Al crear la máquina virtual de SQL Server, tenga en cuenta cómo toocarefully controlar quién tiene máquina toohello de acceso y tooSQL Server. En general, debe realizar los siguientes hello:

- Restringir acceso tooSQL Server tooonly Hola aplicaciones y los clientes que lo necesiten.
- Seguir las prácticas recomendadas para administrar las contraseñas y cuentas de usuario.

Hello las secciones siguientes proporciona sugerencias sobre pensar a través de estos puntos.

## <a name="secure-connections"></a>Conexiones seguras

Cuando se crea una máquina virtual de SQL Server con una imagen de la galería, Hola **conectividad de SQL Server** opción proporciona Hola elección de **locales (dentro de la máquina virtual)**, **privada (dentro de la red Virtual)** , o **público (Internet)**.

![Conectividad de SQL Server](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Para obtener una mayor seguridad hello, elija la opción de más restrictivo de Hola para su escenario. Por ejemplo, si está ejecutando una aplicación que tiene acceso a SQL Server en Hola misma máquina virtual, a continuación, **Local** es la elección más segura de Hola. Si está ejecutando una aplicación de Azure que requiere acceso toohello SQL Server, a continuación, **privada** protege la comunicación tooSQL servidor solo dentro de hello especificado [red Virtual de Azure](../../../virtual-network/virtual-networks-overview.md). Si necesita **público** (internest) acceso toohello VM de SQL Server, a continuación, asegúrese de que toofollow otros procedimientos recomendados en este tema tooreduce el área expuesta a ataques.

Hello opciones seleccionadas en el portal de hello usan reglas de seguridad de entrada en las máquinas virtuales de hello [grupo de seguridad de red](../../../virtual-network/virtual-networks-nsg.md) tooallow (NSG) o denegar la máquina de tooyour de tráfico de red. Puede modificar o crear nuevas reglas NSG entradas puerto de SQL Server tooallow tráfico toohello (predeterminado: 1433). También puede especificar direcciones IP específicas que se permiten toocommunicate a través de este puerto.

![Reglas del grupo de seguridad de red](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

Además de tooNSG reglas toorestrict el tráfico de red, también puede utilizar Hola Firewall de Windows en la máquina virtual de Hola.

Si usas los puntos de conexión con el modelo de implementación clásica de hello, quite cualquier extremo de máquina virtual de hello si no las use. Para obtener instrucciones sobre el uso de ACL con puntos de conexión, consulte [administrar Hola ACL en un punto de conexión](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). Esto no es necesario para las máquinas virtuales que usan Hola, Administrador de recursos.

Por último, considere la posibilidad de habilitar conexiones cifradas para instancia Hola de hello motor de base de datos de SQL Server en la máquina virtual de Azure. Configure la instancia de SQL Server con un certificado firmado. Para obtener más información, consulte [toohello habilitar conexiones cifradas motor de base de datos](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) y [sintaxis de la cadena de conexión](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Usar un puerto no predeterminado

De forma predeterminada, SQL Server escucha en un puerto conocido, 1433. Para aumentar la seguridad, configure toolisten de SQL Server en un puerto no predeterminado, como 1401. Si se aprovisiona una imagen de la Galería de SQL Server en hello portal de Azure, puede especificar este puerto en hello **configuración de SQL Server** hoja.

tooconfigure este después de aprovisionar, tienes dos opciones:

- Para máquinas virtuales del Administrador de recursos, puede seleccionar **configuración de SQL Server** de hoja de información general VM de Hola. Esto proporciona una opción de puerto de hello toochange.

  ![Cambiar el puerto TCP en el portal](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Para máquinas virtuales clásico o para las máquinas virtuales de SQL Server que no se ha aprovisionado con el portal de Hola, puede configurar manualmente el puerto hello mediante la conexión de forma remota toohello máquina virtual. Para pasos de configuración de hello, consulte [configurar una tooListen de servidor en un puerto TCP específico](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). Si utiliza esta técnica manual, deberá tooadd un Firewall de Windows regla tooallow el tráfico entrante en ese puerto TCP.

> [!IMPORTANT]
> Especificación de un puerto no predeterminado es una buena idea si el puerto de SQL Server es toopublic abrir las conexiones a internet.

Cuando SQL Server está escuchando en un puerto no predeterminado, debe especificar el puerto de hello cuando se conecta. Por ejemplo, considere un escenario donde la dirección IP del servidor hello es 13.55.255.255 y SQL Server está escuchando en el puerto 1401. tooconnect tooSQL Server, especificaría `13.55.255.255,1401` en la cadena de conexión de Hola.

## <a name="manage-accounts"></a>Administrar cuentas

No desea nombres de cuenta de estimación de los atacantes tooeasily o contraseñas. Usar hello después toohelp sugerencias:

- Cree una cuenta de administrador local única que no se llame **Administrador**.

- Use contraseñas seguras complejas para todas sus cuentas. Para obtener más información acerca de cómo toocreate una contraseña segura, consulte [crear una contraseña segura](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) artículo.

- De forma predeterminada, Azure selecciona la autenticación de Windows durante la instalación de la máquina virtual de SQL Server. Por lo tanto, Hola **SA** inicio de sesión está deshabilitado y se asigna una contraseña mediante el programa de instalación. Se recomienda que hello **SA** inicio de sesión no se use ni habilitado. Si debe tener un inicio de sesión SQL, utilice uno de hello siguientes estrategias:

  - Cree una cuenta de SQL con un nombre único que sea miembro de **sysadmin**. Puede hacerlo desde el portal de hello habilitando **autenticación de SQL** durante el aprovisionamiento.

    > [!TIP] 
    > Si no habilita la autenticación de SQL durante el aprovisionamiento, debe cambiar manualmente el modo de autenticación de hello demasiado**modo de autenticación de Windows y SQL Server**. Para obtener más información, consulte [Cambiar el modo de autenticación del servidor](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Si tiene que utilizar hello **SA** inicio de sesión, inicio de sesión de Hola a habilitar después de aprovisionamiento y asignar una nueva contraseña.

## <a name="follow-on-premises-best-practices"></a>Seguir las prácticas recomendadas locales

Además toohello procedimientos describen en este tema, se recomienda que revise e implementar prácticas de seguridad locales tradicionales de hello cuando corresponda. Para más información, vea [Consideraciones de seguridad para una instalación de SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).

## <a name="next-steps"></a>Pasos siguientes

Si también está interesado en los procedimientos recomendados de rendimiento, consulte [Procedimientos recomendados para SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-performance.md).

Para ver otros temas relacionados con toorunning SQL Server en máquinas virtuales de Azure, consulte [SQL Server en máquinas virtuales de Azure información general sobre](virtual-machines-windows-sql-server-iaas-overview.md).

