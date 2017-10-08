---
title: 'Azure AD Connect: si ya tiene Azure AD | Microsoft Docs'
description: "En este tema se describe cómo toouse conectarse cuando tiene un inquilino de Azure AD existente."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect: cuando ya hay un inquilino
La mayoría de los temas de Hola para cómo toouse Azure AD Connect se da por supuesto empiezan con un Azure nuevo inquilino de AD y que no hay ningún usuario u otros objetos no existe. Pero si ha iniciado con un inquilino de Azure AD, rellena con los usuarios y otros objetos y ahora desea toouse Connect, a continuación, en este tema es para usted.

## <a name="hello-basics"></a>conceptos básicos de Hola
Un objeto en Azure AD o se controla en la nube (Azure AD) de Hola o de forma local. En el caso de un solo objeto, no puede administrar algunos atributos en un entorno local y otros atributos en Azure AD. Cada objeto tiene una marca que indica donde se administra el objeto de Hola.

Puede administrar algunos usuarios locales y otros en la nube de Hola. Un escenario común de esta configuración es una organización que tiene una combinación de trabajadores de contabilidad y trabajadores de ventas. los trabajadores de contabilidad Hello tener una implementación local no cuenta de AD, pero los trabajadores de ventas de hello, tienen una cuenta de Azure AD. Tendría que administrar algunos usuarios en el entorno local y otros en Azure AD.

Si se inició toomanage a los usuarios en Azure AD que también estén incluidos en AD local y posteriormente desea toouse Connect, a continuación, hay algunas cuestiones adicionales que necesita tooconsider.

## <a name="sync-with-existing-users-in-azure-ad"></a>Sincronización con los usuarios existentes de Azure AD
Cuando instala Azure AD Connect y empezar a sincronizar, hello servicio de sincronización de Azure AD (en Azure AD) realiza una comprobación en cada nuevo objeto e intente toofind un toomatch de objeto existente. Hay tres atributos que se utilizan para este proceso: **userPrincipalName**, **proxyAddresses** y **sourceAnchor**/**immutableID**. Una coincidencia de **userPrincipalName** y **proxyAddresses** se conoce como **coincidencia parcial**. Una coincidencia de **sourceAnchor** se conoce como **coincidencia exacta**. Para hello **proxyAddresses** sólo Hola valor con atributo **SMTP:**, que es la dirección de correo electrónico principal de hello, se utiliza para la evaluación de Hola.

coincidencia de Hola se evalúa solo para los nuevos objetos procedentes de Connect. Si cambia uno que ya exista para que coincida con alguno de estos atributos, verá un error en su lugar.

Si AD Azure busca un objeto que los valores de atributo de hello estén Hola mismo para un objeto procedentes de conectar y todavía está presente en Azure AD, hello objeto en Azure AD toma el conectar. Hello previamente objeto administrado en la nube se marca como administrado en local. Todos los atributos en Azure AD con un valor en el entorno local AD se sobrescriben con valor de hello en local. excepción de Hello es cuando un atributo tiene un **NULL** valor local. En este caso, valor de hello en sigue siendo de Azure AD, pero todavía solo podrá cambiarla local toosomething else.

> [!WARNING]
> Puesto que todos los atributos en Azure AD va toobe sobrescribe el valor local de hello, asegúrese de que dispone de datos en buen estado local. Por ejemplo, si solo tiene una dirección de correo electrónico administrada en Office 365 y no se mantiene actualizada en AD DS local, se pierden todos los valores de Azure AD u Office 365 que no se encuentren en AD DS.

> [!IMPORTANT]
> Si usa la sincronización de contraseñas, que siempre es usar configuración rápida, a continuación, contraseña hello en Azure AD se sobrescribe con la contraseña de hello en el entorno local AD. Si los usuarios son toomanage usa contraseñas diferentes, deberá tooinform que deben usar Hola contraseña local cuando haya instalado conectar.

advertencia y la sección anterior de hello deben considerarse en la planificación. Si ha realizado muchos cambios en Azure AD no se reflejan en local de AD DS, deberá tooplan para cómo toopopulate AD DS con hello actualiza los valores antes de sincronizar los objetos con Azure AD Connect.

Si coinciden los objetos con una coincidencia flexible, Hola **sourceAnchor** se agrega un objeto toohello en Azure AD para una coincidencia de disco duro se puedan utilizar más adelante.

### <a name="hard-match-vs-soft-match"></a>Diferencias entre la coincidencia parcial y la exacta
En una instalación nueva de Connect, apenas las hay. diferencia de Hello está en una situación de recuperación ante desastres. Si su servidor ha perdido la conexión con Azure AD Connect, puede volver a instalar una nueva instancia sin perder datos. Se envía un objeto con un sourceAnchor tooConnect durante la instalación inicial. Hello coincidencia, a continuación, se puede evaluar cliente hello (Azure AD Connect), que es mucho más rápida que hacerlo Hola igual en Azure AD. Las coincidencias exactas las evalúan Connect y Azure AD, y las parciales, Azure AD.

### <a name="other-objects-than-users"></a>Otros objetos distintos a los usuarios
Los usuarios suelen tengan userPrincipalName y proxyAddresses, facilitando la coincidencia de Hola. Sin embargo, otros objetos, como los grupos de seguridad, no los tienen. En este caso, solo puede coincidir con ante una coincidencia de disco duro con hello sourceAnchor. Hola sourceAnchor siempre es hello Base64 convertir **objectGUID** local, por lo que se debe actualizar el valor de hello en Azure AD cuando necesite dos toomatch de objetos. Hola sourceAnchor/immutableID solo pueden actualizarse con PowerShell y no a través de portales de Hola.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Creación de una instancia de Active Directory local a partir de los datos de Azure AD
Algunos clientes comienzan con una solución solo en la nube con Azure AD y no tienen una implementación de AD local. Más adelante desean recursos locales de tooconsume y desea toobuild en local AD basada en datos de Azure AD. Azure AD Connect no puede ayudarlo en este escenario, No crea los usuarios locales y no tiene ningún toohello capacidad tooset Hola contraseña local igual que Azure AD.

Si la única razón de hello ¿por qué piensa tooadd local AD es toosupport LOB (aplicaciones de línea de negocio), quizá debería considerar toouse [servicios de dominio de Azure AD](../../active-directory-domain-services/index.md) en su lugar.

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
