---
title: Azure Active Directory mediante el uso de servicios conectados en Visual Studio aaaAdding | Documentos de Microsoft
description: "Agregar un Azure Active Directory mediante el cuadro de diálogo de Visual Studio agregar servicios conectados Hola"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>Adición de Azure Active Directory con Servicios conectados en Visual Studio
Mediante el uso de Azure Active Directory (Azure AD), puede admitir el inicio de sesión único (SSO) para aplicaciones web ASP.NET MVC o la autenticación de Active Directory en los servicios de API web. Con autenticación de Azure Active Directory, los usuarios pueden usar sus cuentas de aplicaciones web de Azure Active Directory tooconnect tooyour. las ventajas de Hola de autenticación de Azure Active Directory con API Web incluyen seguridad de datos mejorada al exponer una API desde una aplicación web. Con Azure AD, no es necesario toomanage un sistema de autenticación independiente con su propia cuenta y administración de usuario.

## <a name="prerequisites"></a>Requisitos previos
- Cuenta de Azure: si todavía no tiene ninguna cuenta de Azure, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>Conectar Active Directory con servicios conectados de hello tooAzure cuadro de diálogo
1. En Visual Studio, cree o abra un proyecto de ASP.NET MVC o un proyecto de API web de ASP.NET.

1. De hello el Explorador de soluciones, haga clic en hello **servicios conectados** nodo y, en el menú contextual de hello, seleccione **agregar servicios conectados**.

1. En hello **servicios conectados** página, seleccione **autenticación con Azure Active Directory**.
   
    ![Página Servicios conectados](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. En hello **Introducción** página de hello **configuración de Azure AD autenticación** asistente, seleccione **siguiente**.
   
    ![Página de introducción](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. En hello **inicio de sesión único en** página de hello **configuración de Azure AD autenticación** asistente, seleccione un dominio de hello **dominio** lista desplegable. lista de Hola de dominios contiene todos los dominios accesibles por cuentas de hello enumeradas en el cuadro de diálogo de configuración de la cuenta de hello. Como alternativa, puede escribir un nombre de dominio si no encuentra uno que está buscando, como hello `mydomain.onmicrosoft.com`. Puede elegir Hola opción toocreate una aplicación de Azure Active Directory o usar la configuración de Hola desde una aplicación de Azure Active Directory existente. Cuando termine, seleccione **Siguiente**.
   
    ![Página de inicio de sesión único](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. En hello **acceso al directorio** página del programa Hola a **configurar Azure AD Authentication** asistente, asegúrese de que hello **leer datos de directorio** opción está activada. 
   
    ![Página de acceso a directorios](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. Seleccione **finalizar** tooadd Hola a tooenable de código y referencias de configuración necesarios en el proyecto para la autenticación de Azure AD. Puede ver el dominio de Active Directory de hello en hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Visual Studio mostrará un [¿qué ha ocurrido](#how-your-project-is-modified) tooshow artículo también cómo se ha modificado el proyecto. Si desea toocheck que todo funcionó, abra uno de los archivos de configuración de hello modificado y compruebe que configuración de Hola mencionada en el artículo de Hola existen. 

## <a name="how-your-project-is-modified"></a>¿Cómo se modifica el proyecto?
Al ejecutar el Asistente de hello, Visual Studio agrega Azure Active Directory y proyecto de tooyour referencias asociadas. Archivos de configuración y archivos de código en el proyecto también son tooadd modificado compatibilidad con Azure AD. modificaciones específicas de Hola que Visual Studio realiza dependen del tipo de proyecto de Hola. Para información detallada sobre cómo se modifican los proyectos de ASP.NET MVC, consulte [¿Qué ha ocurrido? - Proyectos de MVC](http://go.microsoft.com/fwlink/p/?LinkID=513809). Para los proyectos de API web, consulte [¿Qué ha ocurrido? - Proyectos de API web](http://go.microsoft.com/fwlink/p/?LinkId=513810).

## <a name="next-steps"></a>Pasos siguientes
* [Foro de MSDN para Azure Active Directory](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Documentación de Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Entrada de blog: Introducción tooAzure Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

