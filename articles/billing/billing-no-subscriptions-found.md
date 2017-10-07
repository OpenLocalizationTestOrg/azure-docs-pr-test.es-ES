---
title: las suscripciones de aaaNo error encontraron cuando intente toosign en tooAzure portal o el centro de la cuenta de Azure | Documentos de Microsoft
description: "Proporciona soluciones de Hola para un problema en el que las suscripciones No encontraron el error se produce cuando inicien sesión en el portal de tooAzure o el centro de la cuenta de Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Error No se encontraron suscripciones en Azure Portal o en el Centro de cuentas de Azure
Puede recibir un mensaje de error "No se han encontrado suscripciones" cuando intente toosign en toohello [portal de Azure](https://portal.azure.com/) o hello [centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions). En este artículo se brinda una solución para este problema.

## <a name="symptom"></a>Síntoma

Cuando intente toosign en toohello [portal de Azure](https://portal.azure.com/) o hello [centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions), recibirá Hola siguiente mensaje de error: "No se han encontrado suscripciones".

## <a name="cause"></a>Causa

Este problema se produce si la cuenta no tiene permisos suficientes. 

## <a name="solution"></a>Solución

Asegúrese de que inicie sesión como administrador correcto de Hola. Administrador de la cuenta puede tener acceso a solo el centro de cuentas Hola. Los administradores de servicios (SA) y los coadministradores (CA) tienen acceso permiso solo toohello portal de Azure u Hola portal de Azure clásico.

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a>Escenario 1: Mensaje de Error se recibe en hello [portal de Azure](https://portal.azure.com)

toofix este problema:

* Asegúrese de que ese Hola correcto de directorio de Azure está seleccionada, haga clic en su cuenta en la parte superior de hello derecha.

  ![Directorio de SELECT hello en hello esquina superior derecha del programa Hola a portal de Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* Si hay hello directory derecha Azure seleccionada pero sigue recibiendo un mensaje de error hello [tenga la cuenta que se agrega como un propietario](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Escenario 2: Mensaje de Error se recibe en hello [centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions)

Compruebe si cuenta de hello que usó es Hola Administrador de la cuenta. es tooverify que Hola Administrador de la cuenta, siga estos pasos:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, seleccione **suscripción**.
3. Seleccione la suscripción de Hola que desee toocheck y, a continuación, seleccione **configuración**.
4. Seleccione **Propiedades**. Administrador de la cuenta de suscripción de Hola Hola se muestra en hello **Administrador de la cuenta** cuadro.

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget rápidamente para solucionar el problema. 
