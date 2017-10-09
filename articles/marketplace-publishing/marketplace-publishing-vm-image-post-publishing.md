---
title: "aaaManaging la máquina virtual de la imagen en hello Azure Marketplace | Documentos de Microsoft"
description: "Guía detallada de cómo toomanage la imagen de máquina virtual hello Azure Marketplace después de la publicación inicial"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>Guía de posterior a la producción para la máquina virtual se ofrece en hello Azure Marketplace
Este artículo explica cómo actualizar una oferta de máquina virtual en vivo en hello Azure Marketplace. Le guía a través del proceso de Hola de agregar uno o más nuevo SKU tooan oferta existente. También le guiará Hola proceso de eliminación de una oferta de la máquina virtual en vivo o SKU de hello Marketplace.

Después de una oferta/SKU se almacenan en hello [portal de Azure](http://portal.azure.com), no se puede cambiar Hola siguientes cuadros de texto:

* **Identificador de oferta**: Hola publicación portal, vaya demasiado**máquinas virtuales** y seleccione su oferta. A continuación, haga clic en **IMÁGENES DE LA MÁQUINA VIRTUAL** > **Offer Identifier** (Identificador de oferta).
* **Identificador de SKU**: Hola publicación portal, vaya demasiado**máquinas virtuales** y seleccione su oferta. A continuación, haga clic en **SKU** > **Add a SKU** (Agregar una SKU).
* **Publicador Namespace**: Hola publicación portal, vaya demasiado**máquinas virtuales** > **tutorial** > **saber nos acerca de su empresa** (se encuentra en "Paso 2 registrar su empresa") > **Publisher Namespace** > **Namespace**.

Una vez que aparece en Hola Hola oferta/SKU [Marketplace](http://azure.microsoft.com/marketplace), no se puede cambiar Hola siguientes cuadros de texto:

* **Identificador de oferta**: Hola publicación portal, vaya demasiado**máquinas virtuales** y seleccione su oferta. A continuación, haga clic en **IMÁGENES DE LA MÁQUINA VIRTUAL** > **Offer Identifier** (Identificador de oferta).
* **Identificador de SKU**: Hola publicación portal, vaya demasiado**máquinas virtuales** y seleccione su oferta. A continuación, haga clic en **SKU** > **Add a SKU** (Agregar una SKU).
* **Publicador Namespace**: Hola publicación portal, vaya demasiado**máquinas virtuales** > **tutorial** > **saber nos acerca de su empresa** (se encuentra en "Paso 2 registrar") **Publisher Namespace** > **Namespace**.
* **Puertos**: Hola publicación portal, vaya demasiado**máquinas virtuales** y seleccione su oferta. A continuación, haga clic en **IMÁGENES DE LA MÁQUINA VIRTUAL** > **Open Ports** (Abrir puertos).
* **Pricing Change of listed SKU(s) (Cambio de precios de las SKU activas)**
* **Billing Model Change of listed SKU(s) (Cambio del modelo de facturación de las SKU activas)**
* **Removal of billing regions of listed SKU(s)**
* **Recuento de SKU(s) enumerados de disco de datos que cambian Hola**

## <a name="update-hello-technical-details-of-a-sku"></a>Actualizar detalles técnicos de Hola de una SKU
tooadd un nuevo toohello versión enumerados SKU y volver a publicar su oferta, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **imágenes de máquina virtual** ficha.
4. Hola **SKU** , localice Hola SKU que desea tooupdate.
5. Agregar un nuevo número de versión de Hola SKU y haga clic en hello  **+**  botón. nueva versión de Hello debe tener un formato X.Y.Z, donde X, Y y Z son números enteros. Los cambios de versión solo deben ser incrementales.
6. Hola **dirección URL del VHD OS** cuadro, escriba la firma de acceso compartido de hello identificador URI creado para el sistema de operativo Hola VHD y guardar los cambios de Hola.

   > [!IMPORTANT]
   > No se puede aumentar o disminuir recuento de disco de datos de Hola de una SKU enumerada. En este caso debe toocreate una SKU nuevo. Para obtener instrucciones detalladas, consulte la sección toohello [agregar una SKU nuevo en una oferta enumerada](#add-a-new-sku-under-a-listed-offer).
   >
   >
7. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![Imágenes de máquinas virtuales](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>Actualizar los detalles técnicos de Hola de una oferta o una SKU
Puede actualizar hello no técnicos (marketing, legales, soporte técnico, categorías) detalles de la oferta en vivo o SKU Hola Marketplace.

### <a name="update-hello-offer-description-and-logos"></a>Descripción de la oferta de actualización hello y logotipos
Hola tooupdate detalles de la oferta y volver a publicar su oferta, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **MARKETING** ficha.
4. Haga clic en **Inglés (EU)**.
5. Haga clic en hello **detalles** ficha. Hola **descripción** sección, actualización Hola oferta **título**, **resumen**, y **resumen largo** y guardar los cambios de Hola.

   > [!NOTE]
   > Al actualizar detalles del SKU de hello, tener en cuenta estas restricciones: 
   * No escriba texto duplicado para la descripción de la oferta de Hola y Hola SKU.
   * No escriba texto duplicado para el título de la SKU de Hola y oferta de hello resumida largas. 
   * No escriba texto duplicado para el título de la SKU de Hola y el resumen de oferta de Hola.
   >
   >

    ![Detalles](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. Hola **logotipos** sección de hello **detalles** ficha, actualice los logotipos de Hola. Asegúrese de que los logotipos de hello siguen hello [directrices de Azure Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).

   > [!NOTE]
   > El icono de imagen prominente es opcional. Puede elegir no tooupload un icono héroe. Sin embargo, después de carga un icono héroe, no hay ningún toodelete aprovisionar desde Hola portal de publicación. Siga hello [directrices de icono héroe](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
   >
   >
7. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![Logotipos](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>Hola SKU descripción de la actualización
tooupdate Hola SKU los detalles y volver a publicar su oferta, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **MARKETING** ficha.
4. Haga clic en **Inglés (EU)**.
5. Haga clic en hello **planes** ficha. Hola **SKU** sección, actualice Hola SKU **título**, **resumen**, y **descripción** y guardar los cambios de Hola.

   > [!NOTE]
   > Al actualizar detalles del SKU de hello, tener en cuenta estas restricciones: 
   * No escriba texto duplicado para la descripción de la oferta de Hola y Hola SKU. 
   * No escriba texto duplicado para el título de la SKU de Hola y oferta de hello resumida largas. 
   * No escriba texto duplicado para el título de la SKU de Hola y el resumen de oferta de Hola.
   >
   >
6. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![Planes](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>Cambio de los vínculos existentes o incorporación de nuevos vínculos
toochange los vínculos existentes o agregar nuevos vínculos y, a continuación, volver a publicar su oferta, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **MARKETING** ficha.
4. Haga clic en **Inglés (EU)**.
5. Haga clic en hello **vínculos** ficha.
6. un vínculo nuevo, en hello tooadd **vínculos** sección, haga clic en **+ Agregar vínculo**. Hola **Agregar vínculo** diálogo cuadro, escriba el vínculo de hello **título** y **URL** y guardar los cambios de Hola. Puede escribir cualquier vínculo que contenga información que resulte útil para los clientes.
7. tooupdate o eliminar un vínculo existente, seleccione el vínculo de Hola y haga clic en hello **editar** botón o hello **eliminar** botón.

   > [!NOTE]
   > Asegúrese de que los vínculos de Hola que ya ha escrito en esta sección funcionen correctamente, ya que estos vínculos deben validarse durante el proceso de solicitud de producción.
   >
   >
8. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![Vínculos](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![Agregar vínculo](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>Cambio de una imagen de muestra existente o incorporación de una nueva
toochange un ejemplo existente de la imagen o agregar nuevas imágenes de ejemplo y, a continuación, volver a publicar su oferta, siga estos pasos:

> [!NOTE]
> Imagen de solo ejemplo se muestra en hello [portal de Azure](https://portal.azure.com).
>
>

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **MARKETING** ficha.
4. Haga clic en **Inglés (EU)**.
5. Haga clic en hello **imágenes de ejemplo** ficha.
6. una nueva imagen de ejemplo Hola tooadd **imágenes de ejemplo** sección, haga clic en **cargar una nueva imagen** y guardar los cambios de Hola.

   > [!NOTE]
   > La inclusión de una imagen de muestra es opcional.
   >
7. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![Imágenes de muestra](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Actualizar contenido legal Hola
tooupdate Hola contenido legal y volver a publicar su oferta, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **MARKETING** ficha.
4. Haga clic en **Inglés (EU)**.
5. Haga clic en hello **LEGAL** ficha. Hola **Legal** sección, actualizar sus directivas y condiciones de uso. Escriba o pegue Hola directivas/términos en hello **términos de uso** cuadro y guardar los cambios de Hola.
6. límite de caracteres de Hola de términos legales de Hola de uso es 1 millón de caracteres.
7. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![Información legal](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Actualizar información de soporte técnico de Hola
Hola tooupdate información de soporte técnico y volver a publicar su oferta, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **compatibilidad** ficha.
4. Hola **póngase en contacto con ingeniería** sección Hola ingeniería póngase en contacto con detalles sobre la actualización. Estos detalles se usan para la comunicación interna entre el asociado de Hola y Microsoft solo.
5. Hola **de soporte al cliente** sección, actualice los detalles de contacto de soporte técnico de Hola y Hola **admite la dirección URL**. Estos detalles se usan para la comunicación interna entre el asociado de Hola y Microsoft solo.

   > [!NOTE]
   > Si desea tooprovide solo soporte del correo electrónico, escriba un número de teléfono ficticio en hello **de soporte al cliente** sección. En este caso, el correo electrónico de Hola que proporcionó se utiliza en su lugar.
   >
   >
6. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![Soporte técnico](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>Actualizar las categorías de Hola
tooupdate Hola categorías sección para su oferta y volver a publicar su oferta, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **categorías** ficha.
4. Hola **categorías** sección, actualizar las categorías de Hola para su oferta y guardar los cambios de Hola. Puede elegir las categorías de toofive para Galería de Azure Marketplace de Hola.
5. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
6. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![Categorías](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>Incorporación de una nueva SKU en una oferta activa
tooadd una SKU nuevo en la oferta en vivo, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **SKU** ficha. A continuación, haga clic en **Add a SKU** (Agregar una SKU). 
4. En el cuadro de diálogo de hello, escriba un **identificador de SKU** en minúsculas. Seleccione hello **Traer su propio modelo de facturación de licencia (BYOL)** casilla de verificación si desea que toopublish Hola SKU nuevo con un modelo de facturación de BYOL. En caso contrario, desactive la casilla de verificación de Hola. Haga clic en toocreate de marca de graduación Hola una SKU nuevo. Si no ha elegido el modelo de facturación de hello BYOL, modelo de facturación de Hola se establece automáticamente toohourly. ¿Si desea que la prueba gratuita de 30 días de hello para el modelo de facturación por hora de hello, seleccione **un mes** para **está disponible una prueba gratuita?** De lo contrario, seleccione **No Trial** (Sin prueba). ¿(**Está disponible una prueba gratuita?**  solo aparece si no ha seleccionado BYOL mientras crear Hola SKU nuevo.)

   > [!IMPORTANT]
   > **Ocultar esta SKU de hello Marketplace porque siempre debe ser comprado a través de una plantilla de solución** debe ser **Sí** *sólo* si está aprobado para publicar una plantilla de solución. De lo contrario, esta opción siempre se debe marcar como **No**.
   >
   >
4. En el menú de Hola Hola izquierda, haga clic en hello **imágenes de máquina virtual** ficha y obtenga más información sobre Hola SKU nuevo que ha creado.
5. tooset hasta Hola SKU nueva, vea [obtener la certificación de la imagen VM](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) para obtener instrucciones.
6. tooadd marketing material de Hola SKU nueva, vea [Marketplace proporcionar contenido de marketing](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
7. tooadd información sobre precios de Hola SKU nueva, vea [fijar los precios](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).
8. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

    ![SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![Agregar una SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>Cambiar el número de discos de datos de Hola para una SKU enumerada
No se puede aumentar o disminuir recuento de disco de datos de Hola de una SKU enumerada. En este caso debe toocreate una SKU nuevo. Para obtener instrucciones detalladas, consulte la sección toohello [agregar una SKU nuevo en una oferta enumerada](#add-a-new-sku-under-a-listed-offer).

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Eliminar una oferta enumerada de hello Marketplace
Diversos aspectos necesitan toobe tenerse en cuenta en caso de hello de un tooremove solicitud una oferta en vivo. instrucciones de tooget de tooremove equipo de soporte técnico Hola una oferta enumerada de hello Marketplace, siga estos pasos:

1. Generar una incidencia de soporte técnico en hello [crear un incidente](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) página.

2. Como **tipo de problema**, seleccione **Administrar ofertas**, y como **categoría**, **Modificar una oferta o SKU ya en producción**.
3. Enviar solicitud de saludo.

equipo de soporte técnico de Hello le guía a través del proceso de eliminación de oferta/SKU de Hola.

> [!NOTE]
> Oferta de hello siempre se puede eliminar mientras esté en el estado de borrador (pero no ensayo o producción). En hello **historial** , haga clic en **Descartar borrador**.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Eliminar una lista de SKU de hello Marketplace
toodelete una SKU enumerada de hello Marketplace, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).

2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En panel Hola Hola izquierda, haga clic en hello **SKU** ficha.
4. Seleccione Hola SKU que desee toodelete y haga clic en hello **eliminar** botón.
5. Vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish Hola oferta Hola Marketplace.
6. Después de que se vuelve a publicar oferta Hola Hola Marketplace, Hola SKU se elimina del Marketplace de Hola y Hola portal de Azure.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Eliminar versión actual de Hola de una SKU enumerada de hello Marketplace
versión actual de hello toodelete de una SKU enumerada de hello Marketplace, siga estos pasos: 

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).

2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **imágenes de máquina virtual** ficha.
4. Seleccione Hola SKU cuyo actual versión que desee toodelete y haga clic en hello **eliminar** botón.
5. Vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish Hola oferta Hola Marketplace.
6. Después de oferta de hello obtiene volver a publicar en hello Marketplace, Hola versión actual de hello SKU enumerado se elimina del Marketplace de Hola y Hola portal de Azure. Hola SKU se revierte versión anterior de tooits.

## <a name="revert-hello-listing-price-tooproduction-values"></a>Revertir Hola enumerar valores de precio tooproduction
valores de tooproduction de precio de lista de toorevert hello, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).
2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **precios** ficha.
4. Seleccione una región cuyo precio desee tooreset.

    ![Regiones de precios](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Para SKU con un modelo de facturación por hora, restablecer los precios de Hola para todos los núcleos de hello tal como están en producción para la región seleccionada Hola. Para las SKU con un modelo de facturación de BYOL, asegúrese de Hola SKU disponible en la región de hello seleccionando la casilla de verificación Hola Hola SKU en hello **EXTERNALLY-LICENSED (BYOL) SKU disponibilidad** sección.

    ![Modelos de precios](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. Haga clic en **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**(APLICAR AUTOMÁTICAMENTE LOS PRECIOS PARA ESTADOS UNIDOS A OTROS MERCADOS).

   > [!NOTE]
   > etiqueta del botón Hola puede variar según la región Hola que seleccione. Dado que hemos seleccionado de Estados Unidos, tiene la etiqueta botón Hola **AUTOPRICE otros mercados basándose en los precios en UNITED STATES**.
   >
   >

    ![Aplicar automáticamente los precios](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. En la página 1 del Asistente para Autoprice de hello, elija mercado base hello y haga clic en hello **flecha** botón.

    ![Mercado base](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. En la página 2, elija planes de servicio y metros (núcleos) y haga clic en hello **flecha** botón.

    ![Planes y medidores de servicio](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. En la página 3, haga clic en **Alternar todas** tooselect todas las regiones. O bien, puede seleccionar manualmente las casillas de regiones específicas. Haga clic en hello **flecha** botón.

    ![Elección de mercados](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. En página 4, revise las tasas de cambio de Hola y haga clic en **finalizar**. Asistente de Hello restablece Hola precios selecciones de tooyour correspondiente.

11. En hello **precios** , haga clic en **Ver resumen de los cambios y**.
    En **View Version** (Ver versión), seleccione **Borrador**y en **Comparar con**, seleccione **Producción**. Si no ve ninguna diferencia de precios, precios Hola revierten valores de producción toohello correctamente.

    ![Ver resumen y cambios](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
13. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

## <a name="revert-hello-billing-model-tooproduction-values"></a>Revertir hello tooproduction valores del modelo de facturación
toorevert Hola facturación tooproduction valores del modelo, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).

2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **SKU** ficha.
4. Haga clic en hello **editar** modelo de facturación de botón toorevert Hola. En la ventana de Hola que se abre, active o desactive hello **licencias y facturación se realiza externamente de Azure (también conocido como aportar su propia licencia)** casilla de verificación.

    ![Editar facturación](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. Siga los pasos de hello en "¡hello Revert enumerar valores de precio tooproduction" de este artículo.
6. Vaya toohello **publicar** ficha y haga clic en **tooSTAGING de INSERCIÓN**. Para obtener instrucciones detalladas sobre cómo probar su oferta en el entorno de ensayo de hello, consulte [probar su oferta VM para hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Después de haberlo probado su oferta de almacenamiento provisional, vaya toohello **publicar** ficha Hola portal de publicación. Haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>Revertir la configuración de visibilidad de Hola de un valor de producción de toohello SKU enumerado
configuración de visibilidad de hello toorevert de un valor de producción SKU toohello enumerado, siga estos pasos:

1. Inicie sesión en toohello [portal de publicación](https://publish.windowsazure.com).

2. Vaya toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En el menú de Hola Hola izquierda, haga clic en hello **SKU** ficha.
4. Seleccione el SKU y revertir la configuración de visibilidad de Hola de hello valor SKU toohello producción.

    ![Visibilidad](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. Cuando haya terminado con los cambios de hello, haga clic en **tooPRODUCTION tooPUSH de aprobación de solicitud** toorepublish su oferta en hello Marketplace.

## <a name="see-also"></a>Otras referencias
* [Introducción: Publicar un toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md)
* [Descripción de informes de pago](marketplace-publishing-report-payout.md)
* [Cambio del incentivo de revendedores para proveedores de soluciones en la nube](marketplace-publishing-csp-incentive.md)
* [Solucionar problemas comunes de la publicación en hello Marketplace](marketplace-publishing-support-common-issues.md)
* [Obtención de soporte técnico como publicador](marketplace-publishing-get-publisher-support.md)
* [Creación de una imagen de máquina virtual local](marketplace-publishing-vm-image-creation-on-premise.md)
* [Crear una máquina virtual que ejecuta Windows en el portal de vista previa de Hola](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
