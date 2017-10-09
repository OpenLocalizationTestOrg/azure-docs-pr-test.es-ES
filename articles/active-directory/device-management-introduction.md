---
title: "administración de toodevice aaaIntroduction en Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo la administración de dispositivos puede ayudarle tooget control sobre los dispositivos de Hola que tengan acceso a recursos en su entorno."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Administración de toodevice de introducción en Azure Active Directory

En un mundo móvil en primer lugar, basado en la nube, Azure Active Directory (Azure AD) permite toodevices de inicio de sesión único, las aplicaciones y servicios desde cualquier lugar. Con la proliferación de Hola de dispositivos - incluidos Bring Your Own Device (BYOD), profesionales de TI se enfrentan dos objetivos opuestos:

- Capacitar a toobe de los usuarios finales de hello productivo, donde y cuando
- Proteger los activos corporativos hello en cualquier momento

A través de dispositivos, los usuarios están obteniendo acceso tooyour los activos corporativos. tooprotect los activos corporativos, como un administrador de TI, desea que un control toohave sobre estos dispositivos. Esto le permite toomake seguro de que los usuarios se obtiene acceso a los recursos desde dispositivos que cumplen los estándares de seguridad y cumplimiento de normas. 

Administración de dispositivos también es base hello [acceso condicional basado en dispositivo](active-directory-conditional-access-policy-connected-applications.md). Con el acceso condicional basado en dispositivos, puede asegurarse de que solo es posible con tooresources en su entorno de acceso de confianza para dispositivos.   

En este tema se explica cómo funciona la administración de dispositivos en Azure Active Directory.

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>Dispositivos bajo el control de Hola de Azure AD

tooget un dispositivo bajo el control de Hola de Azure AD, tienes dos opciones:

- Registro 
- Unión

**Registrar** un tooAzure dispositivo AD permite toomanage identidad del dispositivo. Cuando se registra un dispositivo, el registro de dispositivos de Azure AD proporciona dispositivo Hola con una identidad que es usado tooauthenticate Hola dispositivo cuando un usuario inicia sesión tooAzure AD. Puede usar Hola identidad tooenable o deshabilitar un dispositivo.

Cuando se combina con una solución de management(MDM) de dispositivos móviles como Microsoft Intune, los atributos de dispositivo de hello en Azure AD se actualizan con información adicional sobre el dispositivo de Hola. Esto permite que las reglas de acceso condicional de toocreate que exijan el acceso desde dispositivos toomeet los estándares de seguridad y cumplimiento de normas. Para más información sobre la inscripción de dispositivos de Microsoft Intune, consulte el artículo sobre cómo inscribir dispositivos para su administración en Intune.

**Combinar** un dispositivo es un tooregistering de extensión un dispositivo. Esto significa, le proporciona todos los beneficios de Hola de registrar un dispositivo y en suma toothis, también cambia el estado local Hola de un dispositivo. Cambiar el estado local de hello permite que el dispositivo de toosign en tooa de los usuarios mediante una organización cuenta profesional o educativa en lugar de una cuenta personal.

## <a name="azure-ad-registered-devices"></a>Dispositivos registrados en Azure AD   

objetivo de dispositivos de Azure AD registrado Hello es tooprovide con soporte para hello **Bring Your Own Device (BYOD)** escenario. En este escenario, el usuario puede acceder a los recursos controlados de Azure Active Directory de su organización con un dispositivo personal.  

![Dispositivos registrados en Azure AD](./media/device-management-introduction/03.png)

acceso de Hola se basa en una cuenta profesional o educativa que se ha introducido en el dispositivo de Hola.  
Por ejemplo, Windows 10 permite a los usuarios tooadd un trabajo o escuela cuenta tooa PC, Tablet PC o teléfono.  
Cuando un usuario ha agregado un trabajo o la cuenta organizativa, el dispositivo Hola está registrado con Azure AD y opcionalmente inscritos en el sistema de administración (MDM) de dispositivo móvil de Hola que su organización ha configurado. Los usuarios de su organización pueden agregar un trabajo o educativa cómodamente dispositivo personal tooa de cuenta:

- Al obtener acceso a una aplicación de trabajo para hello es la primera vez
- Manualmente a través de hello **configuración** menú en caso de hello de Windows 10 

Puede configurar dispositivos registrados en Azure AD para Windows 10, iOS, Android y macOS.

## <a name="azure-ad-joined-devices"></a>Dispositivos unidos a Azure AD

objetivo de Hola de dispositivos de Azure AD Unido es toosimplify:

- Las implementaciones de Windows de los dispositivos de trabajo 
- Acceso tooorganizational aplicaciones y recursos desde cualquier dispositivo de Windows

![Dispositivos registrados en Azure AD](./media/device-management-introduction/02.png)


Estos objetivos se llevan a cabo proporcionando a los usuarios una experiencia de autoservicio para dispositivos propiedad de trabajo bajo el control de Hola de Azure AD.  
La **unión a Azure AD** está pensada para aquellas organizaciones en las que la nube es prioritaria y exclusiva. Son por lo general pequeñas y medianas empresas que carecen de una infraestructura de Windows Server Active Directory local. 

Implementación de dispositivos de Azure AD unido le ofrece Hola siguientes ventajas:

- **Inicio de sesión único (SSO)** tooyour Azure administra servicios y aplicaciones SaaS. Los usuarios no ven mensajes de autenticación adicionales al acceder a los recursos de trabajo. Hola funcionalidad SSO es incluso cuando no están conectados toohello red de dominio disponible.

- **Itinerancia de las configuraciones de usuario** conforme a la empresa entre dispositivos unidos. Los usuarios no tienen una configuración de toosee de la cuenta (por ejemplo, Hotmail) de Microsoft tooconnect en todos los dispositivos.

- **Acceso tooWindows tienda para empresas** con cuenta de AD. Los usuarios pueden elegir entre un inventario de aplicaciones seleccionadas previamente por organización Hola.

- **Windows Hello** compatibilidad para los recursos de toowork un acceso seguro y práctico.

- **Restricción del acceso** tooapps de solo los dispositivos que cumplen las directivas de cumplimiento.

Aunque la unión a Azure AD esté pensada principalmente para aquellas organizaciones que no tengan una infraestructura de Windows Server Active Directory local, sin duda se puede utilizar también en escenarios donde:

- No puede usar una combinación de dominio local, por ejemplo, si necesita tooget dispositivos móviles como tabletas y teléfonos bajo control.

- Los usuarios necesitan principalmente tooaccess Office 365 u otras aplicaciones de SaaS integradas con Azure AD.

- Desea toomanage un grupo de usuarios en Azure AD en lugar de en Active Directory. Puede aplicar, por ejemplo, los trabajadores tooseasonal, contratistas o estudiantes.

- Desea tooprovide unión capacidades tooworkers en oficinas de sucursales remotas con la infraestructura local limitada.

Puede configurar dispositivos unidos a Azure AD para dispositivos Windows 10.


## <a name="hybrid-azure-ad-joined-devices"></a>Dispositivos híbridos unidos a Azure AD

Para más de una década, muchas organizaciones han utilizado Hola dominio combinación tootheir local Active Directory tooenable:

- TI departamentos toomanage trabajo dispositivos corporativos desde una ubicación central.

- Toosign de usuarios en los dispositivos tootheir con su Active Directory cuentas profesionales o educativas. 

Por lo general, las organizaciones con una superficie local dependen de dispositivos de tooprovision de métodos de imágenes y a menudo usan **System Center Configuration Manager (SCCM)** o **(GP) de directiva de grupo** toomanage ellos.

Si su entorno tiene un servidor local superficie de AD y también desea que aprovechan las capacidades de hello proporcionadas por Azure Active Directory, puede implementar dispositivos de Azure AD unido híbrida. Se trata de dispositivos que son ambos, tooyour unido a Active Directory local y Azure Active Directory.

![Dispositivos registrados en Azure AD](./media/device-management-introduction/01.png)


Debe usar dispositivos híbridos unidos a Azure AD si:

- Tiene dispositivos de implementada toothese de aplicaciones de Win32 que usan NTLM o Kerberos.

- Necesita GP o SCCM / dispositivos de toomanage de DCM.

- Desea que los toocontinue toouse imágenes soluciones tooconfigure dispositivos para los empleados.

Puede configurar dispositivos híbridos unidos a Azure AD para Windows 10 y dispositivos de nivel inferior como Windows 8 y Windows 7.

## <a name="summary"></a>Resumen

Con la administración de dispositivos en Azure AD, puede: 

- Simplificar el proceso de Hola de someter a dispositivos de control de Hola de Azure AD

- Proporcionar a los usuarios con toouse fácil acceso tooyour recursos de una organización basada en la nube

Como regla general, debe utilizar:

- Dispositivos registrados en Azure AD para dispositivos personales

- Azure AD unido dispositivos para dispositivos que no están unidos a un tooan AD local 

- Híbrido Azure AD unido dispositivos para dispositivos que están unidos a un tooan AD local     




## <a name="next-steps"></a>Pasos siguientes

- información general sobre cómo dispositivo toomanage en hello Azure portal, vea tooget [administrar los dispositivos con hello portal de Azure](device-management-azure-portal.md)

- toolearn más sobre el acceso condicional basado en dispositivos, consulte [configurar directivas de acceso condicional basado en dispositivos de Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

- dispositivos de Azure AD unirse de toosetup híbrido, consulte [cómo tooconfigure híbrida Azure Active Directory dispositivos Unidos a un](device-management-hybrid-azuread-joined-devices-setup.md).


