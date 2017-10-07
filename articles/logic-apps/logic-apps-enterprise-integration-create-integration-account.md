---
title: "aaaCreate, link, eliminar o mover una cuenta de integración de aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "¿Cómo toocreate una integración de la cuenta y vincular las aplicaciones lógicas tooyour"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>¿Qué es una cuenta de integración?

Una cuenta de integración permite a las aplicaciones de integración de enterprise toomanage artefactos, incluidos los esquemas, mapas, certificados, socios comerciales y acuerdos. Cualquier aplicación de integración que se crea usa un tooaccess de cuenta de integración estos esquemas, mapas, certificados y así sucesivamente.

## <a name="create-an-integration-account"></a>Creación de una cuenta de integración

1.  Inicie sesión en toohello [portal de Azure](http://portal.azure.com "portal de Azure"). En el menú izquierdo de hello, seleccione **más servicios**.

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. En el cuadro de búsqueda de hello, escriba "integración" para el filtro. En la lista de resultados de hello, seleccione **cuentas de integración**.

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Hola parte superior de la página de hello, elija **agregar**.

    ![Elección de Agregar](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. Nombre de la cuenta de integración y seleccione Hola suscripción de Azure que desea toouse. Puede crear un **Grupo de recursos** nuevo o seleccionar uno existente. A continuación, seleccione la **Ubicación** para hospedar la cuenta de integración y el **Plan de tarifa**. 

    Cuando esté listo, seleccione **Crear**.

    ![Incorporación de los detalles de la cuenta de integración](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure proporciona a su cuenta de integración en la ubicación de hello seleccionado, que debe completarse dentro de 1 minuto.

5. Actualice la página de Hola. Verá la nueva cuenta de integración aparecer en la lista.

    ![La nueva cuenta de integración aparece en la lista](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

A continuación, vincular cuenta de hello de integración que se tooyour creado aplicación lógica. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Vincular una aplicación de la lógica de la cuenta tooa integración

toogive acceso a las aplicaciones lógicas toomaps, esquemas, contratos y otros artefactos de la cuenta de integración, aplicación de vínculo hello integración cuenta tooyour lógica.

### <a name="prerequisites"></a>Requisitos previos

* Tener una cuenta de integración
* Tener una aplicación lógica

> [!NOTE] 
> Asegurarse de que la aplicación de cuenta y la lógica de integración hello *indicarlo Azure* antes de empezar.


1. Hola portal de Azure, seleccione la aplicación lógica y compruebe la ubicación de la aplicación lógica.

    ![Selección de la aplicación lógica y comprobación de la ubicación](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. En **Configuración**, seleccione **Cuenta de integración**.

    ![Selección de la "Cuenta de integración"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. De hello **seleccionar una cuenta de integración** enumerar, cuenta de integración de hello seleccione desea aplicación lógica de toolink tooyour. Elija toofinish vincular, **guardar**.

    ![Selección de la cuenta de integración](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Se recibe una notificación que muestra la integración de cuenta es la aplicación de la lógica de tooyour vinculado, y que todos los artefactos de la cuenta de integración están ahora disponibles tooyour aplicación de lógica.

    ![Se vincula la aplicación lógica tooyour cuenta de integración](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Ahora que su cuenta de integración es aplicación de lógica de tooyour vinculado, puede utilizar conectores de hello B2B en las aplicaciones lógicas. Algunos conectores de B2B comunes incluyen validación XML, y codificación y descodificación de archivos planos.  

## <a name="delete-your-integration-account"></a>Eliminación de la cuenta de integración

1. Seleccione **Más servicios**.

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. En el cuadro de búsqueda de hello, escriba "integración" para el filtro. En la lista de resultados de hello, seleccione **cuentas de integración**.

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Seleccione la cuenta de integración de Hola que desea toodelete.

    ![Seleccione toodelete de cuenta de integración](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. En el menú de hello, elija **eliminar**.

    ![Selección de "Eliminar"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Confirmar la cuenta de integración de hello toodelete choice.

## <a name="move-your-integration-account"></a>Movimiento de la cuenta de integración

toomove un tooanother de cuenta de integración Azure suscripción o grupo de recursos, siga estos pasos.

> [!IMPORTANT]
> Debe actualizar todas las secuencias de comandos toouse Hola nuevos identificadores de recursos después de mover una cuenta de integración.

1. Seleccione **Más servicios**.

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. En el cuadro de búsqueda de hello, escriba "integración" para el filtro. En la lista de resultados de hello, seleccione **cuentas de integración**.

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Seleccione la cuenta de integración de Hola que desea toomove. En **Configuración**, elija **Propiedades**.

    ![Seleccione toomove de cuenta de integración. En Configuración, elija Propiedades.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Cambiar el grupo de recursos de Hola o suscripción de Azure que esté asociada con su cuenta de integración.

    ![Elija Cambiar el grupo de recursos o Cambiar suscripción](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre los contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  

