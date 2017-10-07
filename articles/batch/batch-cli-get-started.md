---
title: aaaGet a trabajar con CLI de Azure para lote | Documentos de Microsoft
description: "Obtenga una introducción rápida toohello comandos del lote de CLI de Azure para administrar los recursos del servicio Azure Batch"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Administración de recursos de Batch con la CLI de Azure

Hola 2.0 de CLI de Azure es la nueva experiencia de línea de comandos de Azure para administrar recursos de Azure. Se puede usar en macOS, Linux y Windows. 2.0 de CLI de Azure está optimizado para administrar recursos de Azure desde la línea de comandos de Hola. Puede usar hello Azure CLI toomanage su cuenta de lote de Azure y sus recursos de toomanage como grupos, los trabajos y tareas. Con hello CLI de Azure, puede crear scripts de muchas de Hola Hola de mismas tareas que llevar a cabo con las API de lote, portal de Azure y cmdlets de PowerShell de lote.

En este artículo se proporciona una introducción al uso de la [CLI de Azure versión 2.0](https://docs.microsoft.com/cli/azure/overview) con Batch. Vea [empezar a trabajar con Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) para obtener información general del uso de hello CLI con Azure.

Microsoft recomienda el uso de la versión más reciente de Hola de hello CLI de Azure, versión 2.0. Para más información acerca de la versión 2.0, consulte [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/) (La línea de comandos de Azure 2.0 está ahora disponible con carácter general).

## <a name="set-up-hello-azure-cli"></a>Configurar Hola CLI de Azure

Hola tooinstall CLI de Azure, siga los pasos de hello descritos en [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).

> [!TIP]
> Le recomendamos que actualice la instalación de CLI de Azure con frecuencia tootake aprovechar las mejoras y las actualizaciones del servicio.
> 
> 

## <a name="command-help"></a>Ayuda de comandos

Puede mostrar texto de ayuda para todos los comandos en hello Azure CLI anexando `-h` toohello comando. Omita el resto de las opciones. Por ejemplo:

* Ayuda de tooget para hello `az` , escriba:`az -h`
* tooget una lista de todos los comandos de proceso por lotes de hello CLI, use:`az batch -h`
* tooget ayuda acerca de cómo crear una cuenta de lote, escriba:`az batch account create -h`

En caso de duda, usar hello `-h` opción de línea de comandos tooget ayuda sobre cualquier comando de CLI de Azure.

> [!NOTE]
> Las versiones anteriores de hello CLI de Azure usa `azure` toopreface un comando CLI. En la versión 2.0, todos los comandos van precedidos de `az`. Ser tooupdate seguro de las scripts toouse Hola nueva sintaxis con la versión 2.0.
>
>  

Además, consulte la documentación de referencia de CLI de Azure de toohello para obtener más información acerca de [comandos de CLI de Azure para lote](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Inicio de sesión y autenticación

Hola toouse CLI de Azure con el lote, necesita toolog en y autenticar. Hay dos toofollow sencillos pasos:

1. **Inicie sesión en Azure.** Iniciar sesión en Azure proporciona acceso a comandos del Administrador de recursos de tooAzure, incluidos los [servicio de administración de lotes](batch-management-dotnet.md) comandos.  
2. **Inicie sesión en su cuenta de Batch.** Iniciar sesión en la le proporciona la cuenta de lote acceder a comandos de servicio de tooBatch.   

### <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Hay unos toolog de distintas maneras en Azure, se describe en detalle en [iniciar sesión con Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Inicie sesión de forma interactiva](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in). Inicie sesión forma interactiva cuando se ejecutan comandos de CLI de Azure desde la línea de comandos de Hola.
2. [Inicie sesión con una entidad de servicio](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal). Inicie sesión con una entidad de servicio cuando ejecute comandos de la CLI de Azure desde un script o una aplicación.

Para fines de Hola de este artículo, le mostramos cómo toolog en Azure interactivamente. Tipo de [inicio de sesión de az](https://docs.microsoft.com/cli/azure/#login) en línea de comandos de hello:

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

Hola `az login` comando devuelve un símbolo (token) que puede usar tooauthenticate, como se muestra aquí. Siga las instrucciones proporcionadas de hello tooopen una página web y enviar Hola token tooAzure:

![Inicie sesión en tooAzure](./media/batch-cli-get-started/az-login.png)

muestran ejemplos de Hello en hello [scripts de shell de ejemplo](#sample-shell-scripts) sección también muestran cómo toostart la sesión de CLI de Azure mediante el registro en Azure de forma interactiva. Una vez que haya iniciado sesión, puede llamar a comandos toowork con recursos de administración de lotes, incluidas las cuentas, las claves, paquetes de aplicaciones y las cuotas de lote.  

### <a name="log-in-tooyour-batch-account"></a>Inicie sesión en tooyour cuenta de lote

toouse hello Azure CLI toomanage lote recursos, como los grupos, los trabajos y las tareas, que necesita toolog en su cuenta de lote y autentica. toolog en toohello servicio por lotes, utilice hello [inicio de sesión de cuenta de lote de az](https://docs.microsoft.com/cli/azure/batch/account#login) comando. 

Tiene dos opciones para autenticarse en su cuenta de Batch:

- **Mediante la autenticación de Azure Active Directory (Azure AD).** 

    Autenticar con Azure AD es predeterminado de hello cuando usas Hola CLI de Azure con el lote y se recomienda para la mayoría de los escenarios. 
    
    Cuando inicie sesión en tooAzure interactivamente, tal y como se describe en la sección anterior de hello, se almacenan en caché en sus credenciales, por lo que Hola CLI de Azure puede iniciar la sesión tooyour con las mismas credenciales de cuenta de lote. Si ha iniciado sesión en tooAzure con una entidad de servicio, esas credenciales también son toolog utilizado en tooyour cuenta de lote.

    Una ventaja de Azure AD es que ofrece control de acceso basado en rol (RBAC). Con RBAC, acceso de un usuario depende de su rol asignado, en lugar de o no poseen claves de cuenta de hello. En lugar de administrar claves de cuenta, puede administrar roles RBAC y dejar que Azure AD se encargue del acceso y la autenticación.  

    Autenticar con Azure AD es necesario si ha creado su cuenta de lote de Azure con su modo de asignación de grupo configurada too'User suscripción '. 

    toolog en tooyour lote cuenta con Azure AD, llame a hello [inicio de sesión de cuenta de lote de az](https://docs.microsoft.com/cli/azure/batch/account#login) comando: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Mediante la autenticación de clave compartida.**

    [La autenticación Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) usa la cuenta acceso claves tooauthenticate comandos de CLI de Azure para hello procesar por lotes de servicio.

    Si va a crear las secuencias de comandos de CLI de Azure tooautomate comandos del lote que realiza la llamada, puede usar la autenticación de clave compartida o una entidad de servicio de Azure AD. En algunos escenarios, puede resultar más sencillo usar la autenticación de clave compartida que crear una entidad de servicio.  

    toolog con la autenticación de clave compartida, incluyen hello `--shared-key-auth` opción en línea de comandos de hello:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

muestran ejemplos de Hello en hello [scripts de shell de ejemplo](#sample-shell-scripts) sección mostrará cómo toolog en su cuenta de lote con Hola CLI de Azure mediante Azure AD y la clave compartida.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Uso de plantillas y transferencia de archivos de la CLI de Azure Batch (versión preliminar)

Puede usar hello Azure CLI toorun lote trabajos-to-end sin escribir código. Archivos de plantilla de proceso por lotes admiten crear grupos, los trabajos y tareas con hello CLI de Azure. También puede usar archivos de entrada de trabajo de hello Azure CLI tooupload toohello cuenta de almacenamiento de Azure asociada con hello cuenta de lote y descargan archivos de salida de trabajo del mismo. Para más información, consulte [Uso de plantillas y transferencia de archivos de la CLI de Azure Batch (versión preliminar)](batch-cli-templates.md).

## <a name="sample-shell-scripts"></a>Scripts de shell de ejemplo

scripts de ejemplo de Hola enumeran en hello siguiente tabla se muestran cómo comandos toouse CLI de Azure con el servicio de lote de Hola y tareas comunes de administración de lotes servicio tooaccomplish. Estas secuencias de comandos de ejemplo tratan muchos de hello comandos disponibles en hello CLI de Azure para el lote. 

| Script | Notas |
|---|---|
| [Crear una cuenta de Batch](./scripts/batch-cli-sample-create-account.md) | Crea una cuenta de Batch y la asocia con una cuenta de almacenamiento. |
| [Agregar una aplicación](./scripts/batch-cli-sample-add-application.md) | Agrega una aplicación y carga los paquetes de binarios.|
| [Administrar grupos de Batch](./scripts/batch-cli-sample-manage-pool.md) | Muestra cómo crear grupos, cambiarlos de tamaño y administrarlos. |
| [Ejecutar un trabajo y tareas con Batch](./scripts/batch-cli-sample-run-job.md) | Muestra cómo ejecutar un trabajo y agregar tareas. |

## <a name="json-files-for-resource-creation"></a>Archivos JSON para la creación de recursos

Al crear recursos de proceso por lotes como grupos y los trabajos, puede especificar un archivo JSON que contiene la configuración del nuevo recurso de hello en lugar de pasar sus parámetros como opciones de línea de comandos. Por ejemplo:

```azurecli
az batch pool create my_batch_pool.json
```

Si bien puede crear más recursos de proceso por lotes utilizando únicamente las opciones de línea de comandos, algunas características requieren que se especifique un archivo con formato JSON que contiene los detalles de recursos de Hola. Por ejemplo, debe usar un archivo JSON si desea que los archivos de recursos de toospecify de una tarea de inicio.

Hola toosee sintaxis de JSON requiere toocreate un recurso, consulte toohello [referencia de la API de REST de lote] [ rest_api] documentación. Cada "agregar *tipo de recurso*" temas de referencia de la API de REST de hello contiene scripts de JSON de ejemplo para la creación de ese recurso. Puede usar los scripts JSON de ejemplo como plantillas para toouse de archivos JSON con hello CLI de Azure. Por ejemplo, hello toosee sintaxis de JSON para la creación de grupo, consulte demasiado[agregar una cuenta del grupo de tooan][rest_add_pool].

Para un script de ejemplo que especifica un archivo JSON, consulte [Ejecutar un trabajo y tareas con Batch](./scripts/batch-cli-sample-run-job.md).

> [!NOTE]
> Si especifica un archivo JSON cuando se crea un recurso, se omite cualquier otro parámetro que especifique en la línea de comandos de Hola para ese recurso.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Consultas eficaces para recursos de Batch

Cada tipo de recurso de proceso de Batch admite un comando `list` que consulta la cuenta de Batch y enumera los recursos de ese tipo. Por ejemplo, puede enumerar grupos de hello en sus cuenta y hello las tareas en un trabajo:

```azurecli
az batch pool list
az batch task list --job-id job001
```

Al consultar el servicio de lote de hello con un `list` operación, puede especificar una cantidad de OData cláusula toolimit Hola de los datos devueltos. Dado que todos los filtros, aparece el servidor, solo los datos de hello que solicitar cruza conexión Hola. Usar estas ancho de banda de cláusulas toosave (y por lo tanto tiempo) al realizar operaciones de lista.

Hello tabla siguiente describen las cláusulas de OData Hola admitidas Hola servicio por lotes:

| Cláusula | Descripción |
|---|---|
| `--select-clause [select-clause]` | Devuelve un subconjunto de propiedades para cada entidad. |
| `--filter-clause [filter-clause]` | Devuelve solo las entidades que coincide con hello especifican expresiones de OData. |
| `--expand-clause [expand-clause]` | Obtiene la información de entidad de hello en una sola llamada REST subyacente. Hola expanda cláusula actualmente admite solo Hola `stats` propiedad. |

Para obtener un ejemplo de script que se muestra cómo toouse una cláusula de OData, vea [ejecutar un trabajo y las tareas con lote](./scripts/batch-cli-sample-run-job.md).

Para obtener más información acerca de cómo realizar consultas de lista eficaz con las cláusulas de OData, vea [consultar el servicio de Azure Batch Hola eficazmente](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Sugerencias de solución de problemas

Hello las sugerencias siguientes pueden ayudarle a cuando esté solucionando problemas de CLI de Azure:

* Use `-h` tooget **texto de Ayuda** para cualquier comando de CLI
* Use `-v` y `-vv` toodisplay **detallado** salida de comandos. Hola cuando `-vv` se incluye la marca, Hola CLI de Azure muestra hello real REST solicitudes y respuestas. Estos modificadores son útiles para mostrar la salida completa del error.
* Puede ver **comando salida JSON** con hello `--json` opción. Por ejemplo, `az batch pool show pool001 --json` muestra las propiedades de pool001 en formato JSON. Luego puede copiar y modificar este toouse de salida en un `--json-file` (consulte [archivos JSON](#json-files) anteriormente en este artículo).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* Hola [foro de lote] [ batch_forum] supervisado por los miembros del equipo de lote. Puede publicar en él sus preguntas si experimenta problemas o desea obtener ayuda acerca de una operación concreta.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información acerca de hello CLI de Azure, vea hello [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).
* Para más información sobre los recursos de Batch, consulte [Introducción a Azure Batch para desarrolladores](batch-api-basics.md).
* Para obtener más información sobre el uso de grupos de plantillas toocreate por lotes, los trabajos y tareas sin escribir código, consulte [usar plantillas de CLI de lote de Azure y transferencia de archivos (vista previa)](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
