---
title: algoritmo de hash de firma de aaaChange de confianza para usuario autenticado de Office 365 | Documentos de Microsoft
description: "En esta página se proporcionan instrucciones para cambiar el algoritmo SHA para la confianza de federación con Office 365."
keywords: "SHA1,SHA256,O365,federación,aadconnect,adfs,ad fs,cambiar sha,confianza de federación,relación de confianza para usuario autenticado"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a>Cambio del algoritmo hash de firma para usuarios de confianza de Office 365
## <a name="overview"></a>Información general
Los servicios de federación de Active Directory (AD FS) se inicia su tooensure de Azure Active Directory de tooMicrosoft de tokens no pueden manipularse. Esta firma se puede basar en SHA1 o SHA256. Azure Active Directory ahora es compatible con tokens firmados con un algoritmo SHA256, y es recomendable establecer tooSHA256 de algoritmo de firma de tokens de Hola de mayor nivel de seguridad de Hola. Este artículo describen pasos Hola necesarios toohello de algoritmo de firma de tokens de Hola de tooset más segura nivel SHA256.

>[!NOTE]
>Microsoft recomienda el uso de SHA256 como algoritmo de Hola para firmar los tokens tal y como es más seguro que SHA1 pero SHA1 sigue siendo una opción admitida.

## <a name="change-hello-token-signing-algorithm"></a>Cambie el algoritmo de firma de tokens de Hola
Después de que ha configurado el algoritmo de firma de hello con uno de los siguientes dos procesos Hola, AD FS firma tokens de Hola para Office 365 relación de confianza con SHA-256. No es necesario toomake los cambios de configuración adicionales, y este cambio no tiene ningún efecto en su tooaccess capacidad Office 365 u otras aplicaciones de Azure AD.

### <a name="ad-fs-management-console"></a>Consola de administración de AD FS
1. Abra la consola de administración de hello AD FS en servidor de hello principal de AD FS.
2. Expanda el nodo de hello AD FS y haga clic en **Veracidades**.
3. Haga clic con el botón derecho en la relación de confianza para usuario autenticado de Office 365 o Azure y seleccione **Propiedades**.
4. Seleccione hello **avanzadas** pestaña y el algoritmo de hash seguro Hola seleccione SHA256.
5. Haga clic en **Aceptar**.

![Algoritmo de firma SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a>Cmdlets de PowerShell de AD FS
1. En cualquier servidor de AD FS, abra PowerShell con privilegios de administrador.
2. Algoritmo de hash seguro conjunto hello mediante el uso de hello **Set-AdfsRelyingPartyTrust** cmdlet.
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a>Consulte también
* [Reparación de la confianza de Office 365 con Azure AD Connect](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

