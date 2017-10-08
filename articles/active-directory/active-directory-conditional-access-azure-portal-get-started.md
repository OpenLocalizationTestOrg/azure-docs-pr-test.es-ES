---
title: aaaGet a trabajar con acceso condicional en Active Directory de Azure | Documentos de Microsoft
description: "Probar el acceso condicional con una condición de ubicación."
services: active-directory
keywords: tooapps de acceso condicional, el acceso condicional con Azure AD, proteger el acceso toocompany recursos, las directivas de acceso condicional
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Introducción al acceso condicional en Azure Active Directory

Acceso condicional es una capacidad de Azure Active Directory que permite toodefine las condiciones en las que los usuarios autorizados pueden tener acceso a las aplicaciones. 

En este tema se proporcionan instrucciones para probar un acceso condicional basado en una condición de ubicación en su entorno.  


## <a name="scenario-description"></a>Descripción del escenario

Un requisito común en muchas organizaciones es tooonly requerir la autenticación multifactor para tooapps de acceso que no se realiza desde la intranet corporativa de Hola. Con Azure Active Directory, puede conseguir este objetivo fácilmente mediante la configuración de una directiva de acceso condicional basado en la ubicación. En este tema se proporcionan instrucciones detalladas para configurar esta directiva. Hola aprovecha la directiva [IP de confianza](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish entre los intentos de acceso de hello corporativa de la intranet y todas las demás ubicaciones.


## <a name="prerequisites"></a>Requisitos previos

Hello escenario descrito en este tema se da por supuesto que está familiarizado con conceptos de Hola que se describen en [acceso condicional de Azure Active Directory](active-directory-conditional-access-azure-portal.md).

tootest este escenario, necesita:

- Crear un usuario de prueba 

- Asignar a un usuario de prueba de toohello de licencia de Azure AD Premium

- Configurar una aplicación administrada y asignar su tooit de usuario de prueba

- Configurar direcciones IP de confianza

Si necesita obtener más información acerca de las direcciones IP de confianza, consulte [Direcciones IP de confianza](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="policy-configuration-steps"></a>Pasos de la configuración de la directiva

**tooconfigure la directiva de acceso condicional, hacer:**

1. Hola portal de Azure, en la barra de navegación izquierdo de hello, haga clic en **Azure Active Directory**. 

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. En hello **Azure Active Directory** hoja en hello **administrar** sección, haga clic en **acceso condicional**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. En hello **acceso condicional** hoja, hello tooopen **New** hoja, en la barra de herramientas de hello en la parte superior de hello, haga clic en **agregar**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. En hello **New** hoja en hello **nombre** cuadro de texto, escriba un nombre para la directiva.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. Hola **asignación** sección, haga clic en **usuarios y grupos**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. En hello **usuarios y grupos** hoja, realizar Hola pasos:

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. Haga clic en **Seleccionar usuarios y grupos**.

    b. Haga clic en **Seleccionar**.

    c. En hello **seleccione** hoja, seleccione el usuario de prueba y, a continuación, haga clic en **seleccione**.

    d. En hello **usuarios y grupos** hoja, haga clic en **realiza**.

7. En hello **New** hoja, hello tooopen **las aplicaciones de nube** hoja en hello **asignación** sección, haga clic en **las aplicaciones de nube**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. En hello **las aplicaciones de nube** hoja, realizar Hola pasos:

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. Haga clic en **Seleccionar aplicaciones**.

    b. Haga clic en **Seleccionar**.

    c. En hello **seleccione** hoja, seleccione la aplicación en la nube y, a continuación, haga clic en **seleccione**.

    d. En hello **las aplicaciones de nube** hoja, haga clic en **realiza**.

9. En hello **New** hoja, hello tooopen **condiciones** hoja en hello **asignación** sección, haga clic en **condiciones**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. En hello **condiciones** hoja, hello tooopen **ubicaciones** hoja, haga clic en **ubicaciones**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. En hello **ubicaciones** hoja, realizar Hola pasos:

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. En **Configurar**, haga clic en **Sí**.

    b. En **Incluir**, haga clic en **Todas las ubicaciones**.

    c. Haga clic en **Excluir** y, después, haga clic en **Todas las direcciones IP de confianza**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. Haga clic en **Done**(Listo).

12. En hello **condiciones** hoja, haga clic en **realiza**.

13. En hello **New** hoja, hello tooopen **Grant** hoja en hello **controles** sección, haga clic en **Grant**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. En hello **Grant** hoja, realizar Hola pasos:

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. Seleccione **Requerir autenticación multifactor**.

    b. Haga clic en **Seleccionar**.

15. En hello **New** hoja, en **habilitar Directiva de**, haga clic en **en**.

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. En hello **New** hoja, haga clic en **crear**.


## <a name="testing-hello-policy"></a>Probar directiva Hola

tootest la directiva, debe tener acceso a la aplicación desde un dispositivo que: 

1. Tener una dirección IP que esté dentro de las direcciones IP de confianza configuradas. 

1. Tener una dirección IP que no esté dentro de las direcciones IP de confianza configuradas.

La autenticación multifactor solo se requerirá durante un intento de conexión realizado desde un dispositivo que no está dentro de las direcciones IP de confianza configuradas. 


## <a name="next-steps"></a>Pasos siguientes

Si desea que toolearn más sobre el acceso condicional, consulte [acceso condicional de Azure Active Directory](active-directory-conditional-access-azure-portal.md).

