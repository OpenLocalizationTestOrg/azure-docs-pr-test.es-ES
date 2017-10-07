---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)
Este artículo muestra cómo tooenable Azure Active Directory Domain Services (Azure AD DS) con Hola portal de Azure.


Hola toolaunch **servicios de dominio de AD de Azure permiten** Hola asistente, completar pasos:

1. Vaya toohello [portal de Azure](https://portal.azure.com).
2. En el panel izquierdo de hello, haga clic en **nuevo**.
3. Hola **New** hoja, escriba **los servicios de dominio** en la barra de búsqueda de Hola.

    ![Buscar servicios de dominio](./media/getting-started/search-domain-services.png)

4. Haga clic en tooselect **servicios de dominio de AD de Azure** de lista de Hola de sugerencias de búsqueda. En hello **servicios de dominio de AD de Azure** hoja, haga clic en hello **crear** botón.

    ![Hoja Servicios de dominio](./media/getting-started/domain-services-blade.png)

5. Hola **servicios de dominio de AD de Azure permiten** se inicia el asistente.


## <a name="task-1-configure-basic-settings"></a>Tarea 1: Configuración básica
Hola **Fundamentos** página del Asistente para hello, puede especificar el nombre de dominio DNS de hello para el dominio administrado Hola. También puede elegir el grupo de recursos de Hola y dominio administrado de ubicación de Azure toowhich Hola debe implementarse.

![Configurar conceptos básicos](./media/getting-started/domain-services-blade-basics.png)

1. Elija hello **nombre de dominio DNS** para el dominio administrado.

   * nombre de dominio predeterminado de Hello del directorio de hello (con un **. onmicrosoft.com** sufijo) se especifica de forma predeterminada.

   * También puede escribir un nombre de dominio personalizado. En este ejemplo, es el nombre de dominio personalizado de hello *contoso100.com*.

     > [!WARNING]
     > prefijo de Hola de su nombre de dominio especificado (por ejemplo, *contoso100* en hello *contoso100.com* nombre de dominio) debe contener 15 caracteres o menos. No puede crear un dominio administrado con un prefijo de más de 15 caracteres.
     >
     >

2. Asegúrese de que ha elegido para hello administrado dominio todavía no existe en la red virtual de hello ese nombre de dominio DNS de Hola. En concreto, compruebe si:

   * Ya tiene un dominio con hello mismo nombre de dominio DNS de red virtual de Hola.

   * red virtual de Hola donde piensa tooenable Hola administrado dominio tiene una conexión VPN con la red local. En este escenario, asegúrese de que no tiene un dominio con hello mismo nombre de dominio DNS de la red local.

   * Tiene un servicio en la nube con ese nombre de red virtual de Hola.

3. Elija hello **tipo de red virtual**. De forma predeterminada, Hola **el Administrador de recursos** está seleccionado el tipo de red virtual. Se recomienda usar este tipo de red virtual para los dominios administrados recién creados.

4. Seleccione hello Azure **suscripción** en el que le gustaría toocreate Hola administrado dominio.

5. Seleccione hello **grupo de recursos** toowhich Hola administrado dominio debe pertenecer. Puede elegir cualquier hello **crear nuevo** o **utilizar existente** grupo de recursos de opciones tooselect Hola.

6. Elija hello Azure **ubicación** en qué Hola se debe crear un dominio administrado. En hello **red** página del Asistente para hello, verá que las redes virtuales solo pertenecen ubicación toohello ha seleccionado.

7. Cuando haya terminado, haga clic en **Aceptar** toomove en toohello **red** página del Asistente para saludo.


## <a name="next-step"></a>Paso siguiente
[Tarea 2: Configuración de red](active-directory-ds-getting-started-network.md)
