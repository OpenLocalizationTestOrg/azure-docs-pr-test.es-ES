---
title: servicios con Visual Studio en la nube aaaManaging roles de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd y quitar roles de Azure servicios en la nube con Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Administración de roles en servicios en la nube de Azure con Visual Studio
Después de haber creado su servicio de nube de Azure, puede agregar nuevos tooit de roles o quitar roles. También puede importar un proyecto existente y convertirlo tooa rol. Por ejemplo, puede importar una aplicación web ASP.NET y designarla como rol web.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>Agregar un tooan de rol Servicio de nube de Azure
Hola pasos le guiarán por agregar un proyecto web o trabajo rol tooan nube de Azure servicio en Visual Studio.

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola

1. Menú contextual hello **Roles** menú contextual del nodo toodisplay Hola. En el menú contextual de hello, seleccione **agregar**, a continuación, seleccione un rol web existente o un rol de trabajo de la solución actual de Hola o crear un proyecto de rol web o de trabajo. También puede seleccionar un proyecto adecuado, por ejemplo, un proyecto de aplicación web ASP.NET, y asociarlo a un proyecto de rol.

    ![Opciones de menú tooadd un proyecto de servicio de rol tooan nube de Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Eliminación de un rol de un servicio en la nube de Azure
Hello siguientes pasos le guiarán quitar un rol web o de trabajo de un proyecto de servicio de nube de Azure en Visual Studio.

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola

1. Expanda hello **Roles** nodo.

1. Menú contextual nodo de hello desea tooremove y, en el menú contextual de hello, seleccione **quitar**. 

    ![Opciones de menú tooadd un tooan de rol Servicio de nube de Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>Volver a agregar un proyecto de servicio de rol tooan nube de Azure
Si quitar una función de su proyecto de servicio de nube, pero más adelante decide tooadd nuevo rol de hello toohello proyecto, solo declaración del rol de Hola y atributos básicos, como los puntos de conexión e información de diagnóstico, se agregan. No hay recursos adicionales o referencias se agregan toohello `ServiceDefinition.csdef` archivo o toohello `ServiceConfiguration.cscfg` archivo. Si desea tooadd esta información, necesita toomanually agregar a estos archivos.

Por ejemplo, puede quitar un rol de servicio web y después decidir tooadd hacer copia de este rol en la solución. Si lo hace, se produce un error. tooprevent este error, tienes hello tooadd `<LocalResources>` elemento mostrado en hello después XML nuevamente en hello `ServiceDefinition.csdef` archivo. Usar el nombre de rol de servicio web de Hola que agregó de nuevo en el proyecto de hello como parte del atributo de nombre de Hola para Hola Hola  **<LocalStorage>**  elemento. En este ejemplo, nombre de Hola Hola web del rol de servicio es **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Pasos siguientes
- [Configurar los Roles de Hola para un servicio de nube de Azure con Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
