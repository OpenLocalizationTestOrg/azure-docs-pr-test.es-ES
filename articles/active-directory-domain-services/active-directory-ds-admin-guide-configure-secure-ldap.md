---
title: aaaConfigure seguro (LDAPS) de LDAP en servicios de dominio de AD de Azure | Documentos de Microsoft
description: "Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services
Este artículo muestra cómo puede habilitar el protocolo ligero de acceso a directorios seguro (LDAPS) para el dominio administrado con Servicios de dominio de Azure AD. LDAP seguro también se denomina "protocolo ligero de acceso a directorios (LDAP) en la Capa de sockets seguros (SSL)/Seguridad de la capa de transporte (TLS)".

## <a name="before-you-begin"></a>Antes de empezar
tareas de hello tooperform enumeradas en este artículo, necesita:

1. Una **suscripción de Azure**válida.
2. Un **directorio de Azure AD** : sincronizado con un directorio local o solo en la nube.
3. **Servicios de dominio de Azure AD** debe estar habilitada para directorio de hello Azure AD. Si lo ha hecho, siga todas las tareas de hello descritas en hello [Guía de introducción](active-directory-ds-getting-started.md).
4. A **tooenable de toobe usa certificado LDAP seguro**.

   * **Recomendado**: obtenga un certificado de una entidad de certificación pública de confianza. Esta opción de configuración es más segura.
   * Como alternativa, también puede elegir demasiado[crear un certificado autofirmado](#task-1---obtain-a-certificate-for-secure-ldap) tal como se muestra más adelante en este artículo.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Requisitos de certificado LDAP seguro Hola
Adquirir un certificado válido por hello siguiendo las directrices, antes de habilitar LDAP seguro. Que se produzcan errores si intenta tooenable LDAP seguro para el dominio administrado con un certificado incorrecto o no es válido.

1. **Emisor de confianza** -certificado Hola debe ser emitido por una entidad de confianza para los equipos que se conectan toohello dominio administrado mediante LDAP seguro. Esta entidad puede ser una entidad de certificación pública de confianza para estos equipos.
2. **Duración** -Hola certificado debe ser válido para al menos hello en los próximos 3 a 6 meses. LDAP acceso tooyour administrado dominio seguro se interrumpe cuando expira el certificado de Hola.
3. **Nombre de sujeto** -nombre de sujeto Hola certificado Hola debe ser un carácter comodín para el dominio administrado. Por ejemplo, si el dominio se denomina 'contoso100.com', nombre de sujeto del certificado de hello debe ser ' *. contoso100.com'. Hola DNS nombre (nombre alternativo del sujeto) toothis comodín nombre del conjunto.
4. **Uso de la clave** - Hola certificado debe configurarse para hello después usa - firmas digitales y cifrado de clave.
5. **Propósito de certificado** -Hola certificado debe ser válido para la autenticación de servidor SSL.

> [!NOTE]
> **Entidades de certificación empresariales:** Azure AD Domain Services no admite el uso de certificados de LDAP seguros emitidos por la entidad de certificación empresarial de su organización. Esta restricción es porque el servicio de hello no confía en la entidad emisora de certificados como una entidad de certificación raíz de empresa. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Tarea 1: Obtener un certificado para LDAP seguro
primera tarea de Hello implica obtener un certificado utilizado para LDAP acceso toohello administrado dominio seguro. Tiene dos opciones:

* Obtención de un certificado de una entidad de certificación. entidad de Hello puede ser una entidad de certificación pública.
* Creación de un certificado autofirmado.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>Opción A (recomendada): obtención de un certificado LDAP seguro desde una entidad de certificación
Si su organización obtiene los certificados de una entidad de certificación pública, deberá tooobtain Hola seguro LDAP de los certificados de esa entidad de certificación pública.

Al solicitar un certificado, asegúrese de cumplir todos los requisitos de hello, que se describen en [requisitos de certificado LDAP seguro hello](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Los equipos cliente que necesitan tooconnect toohello dominio administrado mediante LDAP seguro deben confiar a emisor Hola de certificado LDAP seguro Hola.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Opción B: creación de un certificado autofirmado para LDAP seguro
Si no prevé toouse un certificado de una entidad de certificación pública, puede elegir toocreate un certificado autofirmado para LDAP seguro.

**Creación de un certificado autofirmado con PowerShell**

En el equipo de Windows, abra una nueva ventana de PowerShell como **administrador** y Hola de tipo siga los comandos, toocreate un nuevo certificado autofirmado.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

En el anterior ejemplo de Hola, reemplace '*. contoso100.com' con el nombre de dominio DNS de hello del dominio administrado. Por ejemplo, si ha creado un dominio administrado denominado 'contoso100.onmicrosoft.com', reemplace '*. contoso100.com' Hola por encima de la secuencia de comandos con ' *. contoso100.onmicrosoft.com').

![Selección de un directorio de Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

certificado autofirmado de Hello recién creado se coloca en el almacén de certificados del equipo local de Hola.


## <a name="next-step"></a>Paso siguiente
[Tarea 2: exportar hello tooa de certificado LDAP seguro. Archivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
