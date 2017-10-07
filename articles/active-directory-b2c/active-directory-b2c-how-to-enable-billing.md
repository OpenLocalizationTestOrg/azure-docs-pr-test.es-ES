---
title: "aaaHow tooLink un tooAzure de suscripción de Azure AD B2C | Documentos de Microsoft"
description: "Guía paso a paso tooenable la facturación del inquilino de Azure AD B2C en una suscripción de Azure."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Vincular un toopay de inquilino de Azure B2C de suscripción de Azure tooan de cargos de uso

Los cargos de uso continuo para Azure Active Directory B2C (o Azure AD B2C) son tooan facturación de suscripción de Azure. Es necesario para hello inquilino administrador tooexplicitly vínculo hello Azure AD B2C inquilino tooan suscripción de Azure después de crear el inquilino de hello B2C propio.  Este vínculo se consigue mediante la creación de un anuncio de Azure "B2C inquilino" recurso de destino de hello suscripción de Azure. Muchos inquilinos B2C pueden ser la única suscripción de Azure tooa vinculado junto con otros recursos de Azure (por ejemplo, las máquinas virtuales, almacenamiento de datos, LogicApps)


> [!IMPORTANT]
> Hola información más reciente sobre el uso de facturación y precios para B2C está en hello después de página: [precios de Azure AD B2C](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>Paso 1: Crear un inquilino de Azure AD B2C
Primero se debe completar la creación de un inquilino de B2C. Este paso se puede omitir si ya se ha creado un inquilino de B2C de destino. [Introducción a Azure AD B2C](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>Paso 2: abrir portal de Azure en hello inquilino de Azure AD que muestra su suscripción de Azure
Navegue toohello [portal de Azure](https://portal.azure.com). Cambiar toohello inquilino de Azure AD que muestra hello le gustaría toouse de suscripción de Azure. Este inquilino de Azure AD es diferente del inquilino de hello B2C. Hola portal de Azure, haga clic en nombre de la cuenta de hello en la esquina superior derecha de Hola de Hola Hola de tooselect panel inquilino de Azure AD. Una suscripción de Azure es necesario tooproceed. [Obtención de una suscripción de Azure](https://account.windowsazure.com/signup?showCatalog=True)

![Cambiar tooyour inquilino de Azure AD](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>Paso 3: Crear un recurso B2C Tenant en Azure Marketplace
Abra Marketplace al hacer clic en el icono de Marketplace de hello, o seleccionando Hola verde "+ bien" en hello izquierdo superior del panel de Hola.  Busque y seleccione Azure Active Directory B2C. Seleccione Crear.

![Seleccione Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![Buscar en AD B2C](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

Hola recursos de Azure AD B2C crear Hola de portadas del cuadro de diálogo parámetros siguientes:

1. Inquilino de Azure AD B2C: seleccione un inquilino de Azure AD B2C en lista desplegable de Hola.  Solo se muestran los inquilinos de Azure AD B2C que se pueden elegir.  Aptos inquilinos B2C cumplen estas condiciones: es Hola administrador global del inquilino de hello B2C e inquilino Hola B2C no está asociada actualmente tooan suscripción de Azure

2. Nombre del recurso de AD B2C Azure - es el nombre de dominio de Hola de toomatch preseleccionadas de hello B2C inquilino

3. Suscripción: suscripción activa de Azure en la que es administrador o coadministrador.  Se pueden agregar varios inquilinos de Azure AD B2C tooone suscripción de Azure

4. Ubicación de grupo de recursos y grupo de recursos: este artefacto le ayuda a organizar varios recursos de Azure.  Esta opción no tiene ningún efecto en la ubicación, el rendimiento o el estado de facturación del inquilino de B2C

5. Anclar toodashboard para el inquilino de tooyour B2C acceso más fácil facturación hello y la información de configuración de inquilinos B2C ![crear recursos de B2C](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>Paso 4: Administrar los recursos de inquilino de B2C (opcional)
Una vez completada la implementación, un nuevo recurso de "B2C inquilino" se crea en el grupo de recursos de destino de Hola y relacionados con la suscripción de Azure.  Debería ver que se ha agregado un nuevo recurso del tipo "Inquilino de B2C" a los restantes recursos de Azure.

![Crear recurso de B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

Haciendo clic en recursos del inquilino de hello B2C, es posible
- Haga clic en información de facturación de tooreview de nombre de suscripción. Consulte Facturación y uso.
- Haga clic en configuración de Azure AD B2C tooopen una nueva pestaña de explorador directamente en el inquilino de tooyour B2C hoja de configuración
- Enviar una solicitud de soporte técnico.
- Mover el tooanother de recursos del inquilino B2C suscripción de Azure o tooanother grupo de recursos.  Esta opción cambia la suscripción de Azure que recibe los gastos por uso.

![Configuración de recursos de B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Problemas conocidos
- Eliminación del inquilino de B2C. Si se crea un inquilino B2C, elimina y vuelve a crear con Hola el mismo nombre de dominio, póngase también eliminar y volver a crear el recurso "Vinculación" Hola Hola mismo nombre de dominio.  Esto encontrará "Vincular" recursos en "Todos los recursos" en el inquilino de suscripción de hello mediante Hola portal de Azure.
- Restricciones autoimpuestas en la ubicación del recurso regional.  En raras ocasiones, un usuario puede haber establecido una restricción regional para la creación de recursos de Azure.  Esta restricción puede impedir la creación de hello de hello vínculo entre una suscripción de Azure y un inquilino B2C. toomitigate, por favor, ser menos exigentes con esta restricción.

## <a name="next-steps"></a>Pasos siguientes
Una vez que se han completados estos pasos en cada uno de los inquilinos B2C, la suscripción de Azure se factura según los detalles del Contrato Enterprise o directo de Azure.
- Revisión del uso y facturación en la suscripción de Azure seleccionada
- Revisar los informes detallados de uso de día a día con hello [API de informes de uso](active-directory-b2c-reference-usage-reporting-api.md)
