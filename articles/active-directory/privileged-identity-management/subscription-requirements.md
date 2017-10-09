---
title: "las suscripciones de la administración de identidades de aaaPrivileged - Azure | Documentos de Microsoft"
description: "Explica la suscripción de Hola y requisitos de licencias para administrar y usar Azure AD Privileged Identity Management en su inquilino"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Requisitos de suscripción de Azure Active Directory Privileged Identity Management

AD Privileged Identity Management de Azure está disponible como parte de la edición de hello P2 Premium de Azure AD. Para obtener más información sobre Hola vea otras características de P2 y cómo compara tooPremium P1, [ediciones de Azure Active Directory](../active-directory-editions.md).

>[!NOTE]
Privileged Identity Management de Azure Active Directory (Azure AD) estaba en vista previa, no hay ninguna comprobación de licencia para un servicio de inquilino tootry Hola.  Ahora que Azure AD Privileged Identity Management ha alcanzado la fecha de disponibilidad general, una suscripción de prueba o de pagada debe estar presente para hello inquilino toocontinue con Privileged Identity Management después de diciembre de 2016.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>Confirmación de su suscripción de prueba o de pago

Si no está seguro de si su organización tiene una versión de prueba o adquirir la suscripción, puede comprobar si hay una suscripción en su inquilino mediante el uso de comandos de hello incluidos en Azure Active Directory módulo para Windows PowerShell V1. 
1. Abra una ventana de PowerShell.
2. Escriba `Connect-MsolService` tooauthenticate como un usuario en el inquilino.
3. Escriba `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.

Este comando recupera una lista de suscripciones de hello en el inquilino. Si no hay que ninguna línea devuelve, que necesitará prueba tooobtain un P2 de Azure AD Premium, comprar una suscripción de Azure AD Premium P2 o EMS E5 suscripción toouse AD Privileged Identity Management de Azure.  tooget una versión de prueba y comenzar a usar AD Privileged Identity Management de Azure, lea [empezar a trabajar con Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

Si este comando devuelve una línea en qué SkuPartNumber es "AAD_PREMIUM_P2" o "EMSPREMIUM" y IsTrial es "True", indica que una versión de prueba de Azure AD Premium P2 está presente en el inquilino de Hola.  Si no está habilitado el estado de la suscripción de hello y no tiene una compra de suscripción de Azure AD Premium P2 o E5 de EMS, debe adquirir una suscripción de Azure AD Premium P2 o EMS E5 suscripción toocontinue con Azure AD Privileged Identity Management.

Azure AD Premium P2 está disponible a través de un [contrato Microsoft Enterprise](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), hello [programa de licencias por volumen abierto](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), hello y [programa de proveedores de soluciones de nube](https://partner.microsoft.com/en-US/cloud-solution-provider). Los suscriptores de Azure y Office 365 también pueden comprar Azure AD Premium P2 en línea.  Para obtener más información acerca de precios de Azure AD Premium y cómo se puede encontrar tooorder en línea en [precios de Azure Active Directory](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Azure AD Privileged Identity Management no está disponible en el inquilino

Azure AD Privileged Identity Management ya no estará disponible en el inquilino si:
- Su organización estaba usando Azure AD Privileged Identity Management cuando estaba en versión preliminar y no compra la suscripción de Azure AD Premium P2 o EMS E5.
- Su organización tenía una prueba de Azure AD Premium P2 o EMS E5 que expiró.
- Su organización tenía una suscripción comprada que expiró.

Cuando una suscripción de Azure AD Premium P2 o EMS E5 expira, o una organización que estaba usando Azure AD Privileged Identity Management en versión preliminar no obtiene una suscripción de Azure AD Premium P2 o EMS E5:

- Roles de tooAzure AD de asignaciones de rol permanente se verá afectados.
- Hola extensión de Azure AD Privileged Identity Management Hola portal de Azure, así como cmdlets de API Graph de Hola y las interfaces de PowerShell de AD Privileged Identity Management de Azure, estarán ya no está disponible para los usuarios con privilegios de tooactivate roles, administrar acceso con privilegios, o bien realizar revisiones de acceso de roles con privilegios.
- Como los usuarios ya no será capaz de tooactivate con privilegios roles, se quitarán las asignaciones de roles elegibles de roles de Azure AD.
- Las revisiones de acceso en curso de roles de Azure AD finalizarán y las opciones de configuración de Azure AD Privileged Identity Management se quitarán.
- Azure AD Privileged Identity Management no volverá a enviar correos electrónicos cuando se produzcan cambios de asignación de rol.

## <a name="next-steps"></a>Pasos siguientes

- [Introducción a Privileged Identity Management de Azure AD](../active-directory-privileged-identity-management-getting-started.md)
- [Roles en Privileged Identity Management de Azure AD](../active-directory-privileged-identity-management-roles.md)
