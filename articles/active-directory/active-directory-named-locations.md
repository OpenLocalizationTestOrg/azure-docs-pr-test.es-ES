---
title: ubicaciones de aaaNamed en Azure Active Directory | Documentos de Microsoft
description: "Mediante la configuración de ubicaciones con nombre, puede evitar tener IP direcciones que pertenecen a su organización generan falsos positivos para ubicaciones de hello viaje imposible tooatypical el riesgo de tipo de evento."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Ubicaciones con nombre en Azure Active Directory

Con hello con el nombre de característica de ubicaciones de Azure Active Directory, puede etiquetar los intervalos de direcciones IP de confianza en su organización. En su entorno, puede usar ubicaciones con nombre en el contexto de hello de la detección de Hola de [el riesgo de eventos](active-directory-reporting-risk-events.md). característica de Hello ayuda a reducir el número de Hola de notificado falsos positivos para hello *ubicaciones de viaje imposible tooatypical* el riesgo de tipo de evento. 

## <a name="configuration"></a>Configuración

tooconfigure una ubicación con nombre:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador global.

2. En el panel izquierdo de hello, haga clic en **Azure Active Directory**.

    ![vínculo de Azure Active Directory Hello en el panel izquierdo de Hola](./media/active-directory-named-locations/01.png)

3. En hello **Azure Active Directory** hoja en hello **seguridad** sección, haga clic en **acceso condicional**.

    ![Hola comando de acceso condicional](./media/active-directory-named-locations/05.png)


4. En hello **acceso condicional** hoja en hello **administrar** sección, haga clic en **ubicaciones con nombre**.

    ![Hola comando de ubicaciones con nombre](./media/active-directory-named-locations/06.png)


5. En hello **denominada ubicaciones** hoja, haga clic en **nueva ubicación**.

    ![Hola nuevo comando de ubicación](./media/active-directory-named-locations/07.png)


6. En hello **New** hoja, Hola siguientes:

    ![Nueva hoja de Hola](./media/active-directory-named-locations/08.png)

    a. Hola **nombre** , escriba un nombre para la ubicación con nombre.

    b. Hola **intervalos IP** , escriba un intervalo de IP. intervalo IP de Hello necesita toobe Hola *enrutamiento de interdominios sin clase* formato (CIDR).  

    c. Haga clic en **Crear**.



## <a name="what-you-should-know"></a>Qué debería saber

**Actualización masiva**: al crear o actualizar las ubicaciones con nombre, para las actualizaciones masivas, puede cargar o descargar un archivo CSV con intervalos IP de Hola. Una carga agrega intervalos IP de hello en lista de hello archivos toohello en lugar de sobrescribir la lista de Hola.

![Hola, cargar y descargar vínculos](./media/active-directory-named-locations/09.png)


**Limitaciones**: puede definir un máximo de 60 ubicaciones con nombre, con un tooeach de rango asignado de IP de ellos. Si tiene una sola ubicación con nombre configurada, puede definir intervalos IP too500 para él.


## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de los eventos de riesgo, vea [eventos de riesgo de Azure Active Directory](active-directory-reporting-risk-events.md).

