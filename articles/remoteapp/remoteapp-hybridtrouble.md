---
title: "aaaTroubleshoot crear colecciones de RemoteApp híbrida | Documentos de Microsoft"
description: "Obtenga información acerca de cómo errores de creación de colección de tootroubleshoot RemoteApp híbrida"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Solución de problemas de creación de colecciones híbridas de Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Una colección híbrida se hospeda en y almacena los datos en la nube de Azure Hola pero también permite a los usuarios obtener acceso a datos y recursos almacenados en la red local. Los usuarios pueden acceder a las aplicaciones mediante el inicio de sesión con sus credenciales corporativas sincronizadas o federadas con Azure Active Directory. Puede implementar una colección híbrida que use una red virtual de Azure existente o bien puede crear una nueva red virtual. Se recomienda crear o utilizar una subred de red virtual con un rango de CIDR lo suficientemente grande como para cubrir el crecimiento futuro esperado para Azure RemoteApp.

¿Todavía no ha creado la colección? Vea [crear una colección híbrida](remoteapp-create-hybrid-deployment.md) para conocer los pasos Hola.

Si tiene problemas para crear la colección, o si no funciona la colección de hello forma Hola piensa que debería, desproteger Hola siguiente información.

## <a name="your-image-is-invalid"></a>La imagen no es válida
Si ve un mensaje como "GoldImageInvalid" cuando se está esperando tooprovision Azure la colección, significa que la imagen de plantilla no cumple con hello [define los requisitos de la imagen](remoteapp-imagereqs.md). Por lo tanto, vaya a leerlos [requisitos](remoteapp-imagereqs.md), corrija la imagen e inténtelo de toocreate volver a la colección.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>¿La red virtual tiene grupos de seguridad de red definidos?
Si tiene definidos en la subred de Hola se usan para la colección de grupos de seguridad de red, asegúrese de que estos [puertos y direcciones URL](remoteapp-ports.md) son accesibles desde dentro de la subred.

Puede agregar otra red seguridad grupos toohello máquinas virtuales implementadas por el usuario en la subred de Hola para un control más estricto.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>¿Utiliza sus propios servidores DNS? ¿Son accesibles desde la subred de red virtual?
> [!NOTE]
> Tiene toomake Hola seguro de los servidores DNS en la red virtual siempre están funcionando y máquinas virtuales siempre pueda tooresolve Hola que hospedados en hello red virtual. No utilice Google DNS para ello.
> 
> 

En las colecciones híbridas utiliza sus propios servidores DNS. Especifica estos recursos en el esquema de configuración de red o a través del portal de administración de hello cuando se crea la red virtual. Se usan servidores DNS en orden de Hola que se especifican en forma de conmutación por error (como tooround opuestos Round robin).  
Consulte demasiado[resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake que los servidores DNS estén configurado correcly.

Asegúrese de que los servidores DNS de hello de la colección están accesibles y está disponible en la subred de red virtual de hello especificado para esta colección.

Por ejemplo:

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definir el DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>¿Utiliza un controlador de dominio de Active Directory en la colección?
Actualmente solo se puede asociar un dominio de Active Directory con Azure RemoteApp. colección de Hello híbrida admite solo las cuentas de Azure Active Directory que se han sincronizado con la herramienta de sincronización de directorios de una implementación de Windows Server Active Directory; en concreto, o bien se sincronizan con la opción de sincronización de contraseña de Hola o sincronizados con la federación de servicios de federación de Active Directory (AD FS) configurada. Es necesario toocreate un dominio personalizado que coincide con el sufijo de dominio UPN de hello para el dominio local y configurar la integración de directorio.

Consulte [Configuración de Active Directory para Azure RemoteApp](remoteapp-ad.md) para obtener información.

Asegúrese de que detalles del dominio Hola proporcionadas son válidas y controlador de dominio de hello sea accesible desde Hola que VM creada en la subred de hello usada para la aplicación de Azure remota. Compruebe también que la cuenta de servicio de hello las credenciales proporcionadas tienen permisos tooadd equipos toohello proporcionado por el dominio y que Hola nombre AD siempre se puede resolver de hello DNS proporcionado en hello red virtual.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>¿Qué nombre de dominio especificó al crear la colección?
nombre de dominio de Hello creen o agreguen debe ser un nombre de dominio interno (no el nombre de dominio de Azure AD) y debe estar en un formato DNS (contoso.local). Por ejemplo, tiene un nombre interno de Active Directory (contoso.local) y un UPN de Active Directory (contoso.com) - tiene el nombre interno de hello toouse cuando se crea la colección.

