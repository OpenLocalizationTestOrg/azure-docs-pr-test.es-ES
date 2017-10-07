---
title: 'Azure Active Directory B2C: atributos personalizados | Microsoft Docs'
description: "Funcionamiento de atributos personalizado toouse en Azure Active Directory B2C toocollect información acerca de los consumidores"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Azure B2C Directory Active: Usar la información toocollect atributos personalizados acerca de los consumidores
El directorio de Azure Active Directory (Azure AD) B2C incluye un conjunto integrado de información (atributos): Nombre propio, Apellido, Ciudad, Código postal y otros atributos. Sin embargo, cada aplicación de consumo tiene requisitos únicos en qué toogather atributos de los consumidores. Con Azure AD B2C, se puede extender el conjunto de Hola de atributos que se almacenan en cada cuenta de cliente. Puede crear atributos personalizados en hello [portal de Azure](https://portal.azure.com/) y utilizarlo en las directivas de inicio de sesión, como se muestra a continuación. También puede leer y escribir estos atributos mediante hello [API de Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Los atributos personalizados usan las [Extensiones de esquema de directorio de la API de Azure AD Graph](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Creación de un atributo personalizado
1. [Siga estos módulos de características de pasos toonavigate toohello B2C en hello portal de Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Haga clic en **Atributos de usuario**.
3. Haga clic en **+ agregar** princip Hola de hoja de Hola.
4. Proporcionar un **nombre** para el atributo personalizado de hello (por ejemplo, "ShoeSize") y, opcionalmente, un **descripción**. Haga clic en **Crear**.
   
   > [!NOTE]
   > Solo Hola "String" **tipo de datos** está disponible actualmente.
   > 
   > 

atributo personalizado de Hello ahora está disponible en la lista de Hola de **atributos de usuario**y para su uso en las directivas de inicio de sesión.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Uso de un atributo personalizado en la directiva de registro
1. [Siga estos módulos de características de pasos toonavigate toohello B2C en hello portal de Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Haga clic en **Directivas de registro**.
3. Haga clic en la directiva de inicio de sesión (por ejemplo, "B2C_1_SiUp") tooopen. Haga clic en **editar** princip Hola de hoja de Hola.
4. Haga clic en **atributos suscripción** y atributos personalizados de hello seleccione (por ejemplo, "ShoeSize"). Haga clic en **Aceptar**.
5. Haga clic en **notificaciones de la aplicación** y atributos personalizados de hello select. Haga clic en **Aceptar**.
6. Haga clic en **guardar** princip Hola de hoja de Hola.

Puede usar la característica de "Ejecutar ahora" hello en la experiencia del consumidor de hello directiva tooverify Hola. Ahora debe vea "ShoeSize" en lista de Hola de atributos que se recopila durante el inicio de sesión del consumidor y verlo en la aplicación de hello token tooyour atrás enviado.

## <a name="notes"></a>Notas
* Junto con las directivas de registro, los atributos personalizados también se pueden utilizar en las directivas de registro o inicio de sesión y en las directivas de edición del perfil.
* Hay un límite conocido de atributos personalizados. Es solo crea Hola primera vez que se utiliza en las directivas de, y no cuando se agrega lista toohello de **atributos de usuario**.

