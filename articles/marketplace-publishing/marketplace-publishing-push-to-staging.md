---
title: "aaaPrepare y probar su oferta de implementación toohello Azure Marketplace | Documentos de Microsoft"
description: Instrucciones detalladas en proporcionar contenido de marketing, configurar planes de precios y probar su oferta antes de implementar toohello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3ccd2448-895b-477e-adf6-ab655a21d2fa
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/17/2016
ms.author: hascipio
ms.openlocfilehash: 04f142c2dc894716c187751736549586c24a9d01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-offer-creation-with-marketing-content"></a>Hola completa ofrecen creación con contenido de marketing
En este paso del proceso de publicación de hello, necesitará tooprovide ciertos marketing contenido y detalles acerca de la oferta o SKU en hello Azure Marketplace. Por ejemplo, proporcionará una descripción de su producto, logotipos de empresa, planes de precios, detalles de los planes y otro toopush es necesario obtener información su oferta y/o toostaging SKU. Esta información se utiliza como contenido de marketing de hello portal de Azure. Se iniciará este proceso en hello [portal de publicación][link-pubportal].

## <a name="step-1-provide-marketplace-marketing-content"></a>Paso 1: Especificación de contenido de marketing de Marketplace
**El inglés es el predeterminado de Hola y solo admite el idioma.** Asegúrese de que toda la información proporcionada en los campos de hello esté en inglés. Toda la información puede modificarse en cualquier momento hasta que pulse toostaging.

1. Vaya toohello publicación portal, [https://publish.windowsazure.com](https://publish.windowsazure.com).
2. En el menú de la izquierda hello, haga clic en hello **Marketing** ficha.
3. En el panel principal de hello, haga clic en hello **inglés (Estados Unidos)** botón.
   
   > [!IMPORTANT]
   > Todos los campos deben tener sus entradas, incluidas las imágenes de hello, para toostaging toopush capaz de toobe.
   > 
   > 

### <a name="details-and-plans"></a>Detalles y planes
1. Escriba el título de la oferta de hello (50 caracteres como máximos), ofrecen resumen (100 caracteres como máximos), ofrecen resumen largo (256 caracteres como máximos), descripción (máximo 1300 caracteres), los logotipos en hello de la oferta **detalles** ficha
2. Escriba plan título (máximo de 50 caracteres), resumen del plan (100 caracteres como máximos), descripción (máximo 2000 caracteres) en hello del plan **planes** ficha.
   
   > [!NOTE]
   > Puede usar Hola después HTML tooformat Hola resumen de etiquetas, resumida largas y la descripción de la oferta de Hola y planes. Hola permitidos etiquetas HTML son h1, h2, h3, h4, h5, p, ol, ul, li, un [destino | href] segura, em, b,.
   > 
   > 
3. No escriba texto duplicado en la descripción del plan y la oferta.
4. No escriba texto duplicado en el resumen largo de la oferta y el título del plan.
5. No escriba texto duplicado en el resumen de la oferta y el título del plan.
6. No escriba títulos de planes idénticos en una oferta con varios planes.
7. Cargar imágenes de especificaciones de hello necesario (mencionadas en el Portal de publicación de Hola) en formato PNG, uno para cada tamaño.
8. Asegúrese de que los logotipos de hello siguen hello Azure Marketplace las directrices para logotipos que se mencionan más abajo.
   
   ![dibujo](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-details-02.png)

**Instrucciones del logotipo de Azure Marketplace**

Todos los logotipos de hello en el Portal de publicación de hello deben seguir hello debajo de instrucciones:

* Hola diseño de Azure tiene una paleta de colores simple. Mantener número Hola de principal y los colores de la base de datos secundaria en el logotipo baja.
* colores del tema Hola de hello portal de Azure son blancos y negros. Por lo tanto, evite usar estos colores como color de fondo de Hola de los logotipos. Usar algunos colores que podría hacer que sus logotipos destacan en hello portal de Azure. Nosotros recomendamos usar colores primarios simples. **Si está usando un fondo transparente, asegúrese de que ese Hola logotipos o texto no son blanco o negro o azul.**
* No utilice un fondo degradado en logotipo Hola.
* Evite colocar texto, incluso la empresa o el nombre de marca, en el logotipo de Hola. Hola apariencia y funcionamiento de su logotipo debe ser "plano" y debe evitar degradados.
* logotipo de Hello no debe ajustarse.
* El logotipo pequeño debe tener un tamaño de 40 x 40 píxeles
* El logotipo mediano debe tener un tamaño de 90 x 90 píxeles
* El logotipo grande debe tener un tamaño de 115 X 115 píxeles
* El logotipo ancho debe tener un tamaño de 255 X 115 píxeles
* El logotipo de imagen prominente debe tener un tamaño de 815 X 290 píxeles

> [!NOTE]
> logotipo de héroe de Hello es opcional. publicador de Hello puede elegir no tooupload un logotipo héroe. Sin embargo cuando se han cargado Hola héroe icono no se puede eliminar de hello portal de publicación. En ese momento, socio Hola debe seguir instrucciones de Azure Marketplace de Hola para iconos héroe.
> 
> 

  ![dibujo](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-details-03.png)

**Instrucciones adicionales para el icono del logotipo de hello héroe (opcional)**

* logotipo de héroe de Hello es opcional. publicador de Hello puede elegir no tooupload un logotipo héroe. **Sin embargo cuando se han cargado Hola héroe icono no se puede eliminar de hello portal de publicación. En ese momento, socio Hola debe seguir instrucciones de Azure Marketplace de Hola por iconos héroe else oferta hello no será posible tooproduction aprobada.**
* Hola publicador nombre para mostrar, plan hello y título ofrecen resumen largo se muestran en color de fuente blanca. Por lo tanto, debe evitar mantener cualquier color claro en fondo Hola Hola héroe icono. Los fondos transparentes y de color negro y blanco no pueden utilizarse en las imágenes prominentes.
* publicador de Hello nombre para mostrar, título, resumidas largas de oferta de Hola y Hola botón para crear el plan se incrustan mediante programación dentro de hello logotipo héroe una vez que la oferta de hello queda enumerada. Por lo que no debe escribir cualquier texto mientras se diseñan logotipo héroe de Hola. Deje espacio vacío en hello derecho puesto hello texto (es decir, Mostrar nombre del publicador, título de plan, oferta Hola resumida largas) se incluirán mediante programación con nosotros a través de allí. espacio vacío de Hola para texto hello debe ser 415 x 100 en hello derecho (y se desplaza por 370px de hello izquierda).
  
  ![dibujo](media/marketplace-publishing-push-to-staging/pubportal-herobanner.png)

### <a name="links"></a>Vínculos
En hello **vínculos** ficha barra izquierda hello, especifique los vínculos con información que puede ayudar a los clientes. Escriba un nombre y una dirección URL para cada vínculo.

![dibujo](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-link-01.png)

### <a name="sample-images-optional"></a>Imágenes de ejemplo (opcional)
> [!NOTE]
> La inclusión de una imagen de ejemplo es un paso opcional.
> Aunque puede cargar varias imágenes de ejemplo de Hola publicar portal, solamente una imagen (seleccionada al azar por sistema Hola) se muestra en hello portal de Azure. Por este motivo, recomendamos cargar, como mínimo, una imagen de ejemplo.
> 
> 

En hello **imágenes de ejemplo** ficha en el menú de la izquierda hello, cargar una nueva imagen, haga clic en **cargar una nueva imagen**. Si tiene una imagen existente y le gustaría tooreplace, haga clic en **Reemplazar imagen**.

![dibujo](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-sampleimg-01.png)

### <a name="legal"></a>Información legal
En hello **Legal** ficha, proporcione un vínculo tooyour directivas y condiciones de uso. Escriba o pegue términos Hola Hola grandes **términos de uso** cuadro. Hola límite para condiciones legales de Hola de uso es 1.000.000 caracteres.

![dibujo](media/marketplace-publishing-push-to-staging/pubportal-marketingcontent-legal-01.png)

**Nota:** para las ofertas de la máquina Virtual, una vez que una oferta/SKU está representado en hello Portal de Azure, no se puede cambiar los campos de hello indicados a continuación:

* **Offer Identifier** (Identificador de oferta): Portal de publicación -&gt; Máquinas virtuales -&gt; Select your Offer (Seleccionar oferta) -&gt; pestaña Imágenes de VM -&gt; Offer Identifier (Identificador de oferta)
* **SKU Identifier** (Identificador de SKU): Portal de publicación -&gt; Máquinas virtuales -&gt; Select your Offer (Seleccionar oferta) -&gt; pestaña SKUs (SKU) -&gt; Offer Identifier (Identificador de oferta)
* **Publisher Namespace** (Espacio de nombres de publicador): Portal de publicación -&gt; Máquinas virtuales -&gt; pestaña Walkthrough (Tutorial) -&gt; Tell Us About Your Company (Indíquenos la información de su empresa) (esta opción se encuentra en el paso 2 sobre registro de la empresa) -&gt; Publisher Namespace (Espacio de nombres de publicador) -&gt; Espacio de nombres

Para las ofertas de la máquina Virtual, una vez que se muestra hello oferta/SKU en hello Azure Marketplace, no se puede cambiar los campos de hello indicados a continuación:

* **Offer Identifier** (Identificador de oferta): Portal de publicación -&gt; Máquinas virtuales -&gt; Select your Offer (Seleccionar oferta) -&gt; Imágenes de VM -&gt; Offer Identifier (Identificador de oferta)
* **SKU Identifier** (Identificador de SKU): Portal de publicación -&gt; Máquinas virtuales -&gt; Select your Offer (Seleccionar oferta) -&gt; pestaña SKUs (SKU) -&gt; Offer Identifier (Identificador de oferta)
* **Publisher Namespace** (Espacio de nombres de publicador): Portal de publicación -&gt; Máquinas virtuales -&gt; pestaña Walkthrough (Tutorial) -&gt; Tell Us About Your Company (Indíquenos la información de su empresa) (esta opción se encuentra en el paso 2 sobre registro) -&gt; Publisher Namespace (Espacio de nombres de publicador) -&gt; Espacio de nombres
* **Puertos**: Portal de publicación -&gt; Máquinas virtuales -&gt; Select your Offer (Seleccionar oferta) -&gt; pestaña Imágenes de VM -&gt; Open Ports (Abrir puertos)
* **Pricing Change of listed SKU(s)**
* **Billing Model Change of listed SKU(s)**
* **Removal of billing regions of listed SKU(s)**
* **Recuento de SKU(s) enumerados de disco de datos que cambian Hola**

## <a name="step-2-set-your-prices"></a>Paso 2: Establecimiento de precios
### <a name="pricing-models"></a>Modelos de precios
| Modelo de precios | Descripción |
| --- | --- |
| Base |Tarifa plana mensual que se paga en el momento de la compra; por ejemplo, 10 $/mes |
| Consumo (también conocido como "medidor de uso") |Pago por uso, que se define por publicador Hola de oferta de Hola. No se puede definir por encima del límite por puesto, por usuario, etc., porque no hay ningún concepto de una fracción de un usuario o proration toodo de capacidad. Se informa del uso socio Hola cada hora. El cliente paga en hello del ciclo de facturación mensual, como principio tooup lugar como planes mensuales. |
| Evaluación gratuita |El cliente puede usarla de forma gratuita durante un tiempo limitado y pagará tarifas normales a partir de entonces. |
| Nivel Gratis |El plan es siempre gratuito. |
| Migración (también conocido como "actualización" o "degradación") del plan |Concepto de un usuario estaba moviendo desde su plan tooanother aceptable plan actual; definido por el socio comercial. |

**Modelos de precios disponibles por tipo de oferta**

> [!IMPORTANT]
> La disponibilidad de ciertos modelos de precios varía según el tipo de la oferta. Vea la siguiente tabla de Hola.
> 
> 

|  | Solo base | Solo consumo | Base y consumo |
| --- | --- | --- | --- |
| Imagen de máquina virtual |No |Sí |No |
| Servicio de desarrolladores |Sí |Sí |Sí |

### <a name="21-set-your-vm-prices"></a>2.1. Establecimiento de los precios de máquina virtual
Actualmente para máquinas virtuales, tenemos siguiente hello **3 tipos de modelos de facturación:**

* **Cada hora:** se le cobre los clientes de forma por hora en función de las tasas de hello establecidas por los publicadores de hello en tamaños de máquinas virtuales de Hola. En caso de **facturación horaria** modelo de hello las SKU de precio total de hello estará suma Hola Hola software costo cobrado por hello hello y publicador infraestructura costo cobrado por Microsoft. Este costo total será cliente toohello mostrado como un precio por hora y mensual cuando considere la compra de hello (consulte la siguiente captura de pantalla de hello). **Publicador recibe el 80% del costo de software de hello cobrado por ellos.** Por lo tanto, asegúrese de cálculo de hello en consecuencia antes de establecer los precios para las SKU.
  
    ![dibujo](media/marketplace-publishing-push-to-staging/img2.1-01.png)
* **Prueba gratuita:** se trata de otro tipo de modelo de Hola por hora. Aquí cliente hello no se le cobre por costo de software para hello days(Free) 30 primeros después de implementar VM Hola. Después de 30days cobran según una por hora en función de las tasas de hello establecidas por publicadores hello en el modelo por hora de Hola.
* **Bring-Your-posee-licencia (BYOL):** publicadores Hola administración hello las licencias de software de Hola que se ejecuta en hello VM.

**Importante:** cuando aparece Hola oferta/SKU en hello Azure Marketplace, no puede cambiar los campos de hello indicados a continuación.

* **Pricing Change of listed SKU(s)**
* **Billing Model Change of listed SKU(s)**
* **Removal of billing regions of listed SKU(s)**
* **Recuento de SKU(s) enumerados de disco de datos que cambian Hola**
* **Offer Identifier** (Identificador de oferta): Portal de publicación -&gt; Máquinas virtuales -&gt; Select your Offer (Seleccionar oferta) -&gt; Imágenes de VM -&gt; Offer Identifier (Identificador de oferta)
* **SKU Identifier** (Identificador de SKU): Portal de publicación -&gt; Máquinas virtuales -&gt; Select your Offer (Seleccionar oferta) -&gt; pestaña SKUs (SKU) -&gt; Offer Identifier (Identificador de oferta)
* **Publisher Namespace** (Espacio de nombres de publicador): Portal de publicación -&gt; Máquinas virtuales -&gt; pestaña Walkthrough (Tutorial) -&gt; Tell Us About Your Company (Indíquenos la información de su empresa) (esta opción se encuentra en el paso 2 sobre registro) -&gt; Publisher Namespace (Espacio de nombres de publicador) -&gt; Espacio de nombres
* **Puertos**: Portal de publicación -&gt; Máquinas virtuales -&gt; Select your Offer (Seleccionar oferta) -&gt; pestaña Imágenes de VM -&gt; Open Ports (Abrir puertos)

### <a name="sell-to-countries-of-hello-sku"></a>"Ventas para" países de hello SKU
Necesita toocarefully tenga en cuenta que le proporcione las SKU. Algunos países se clasifican como Microsoft remit (Envío por parte de Microsoft) y otros como ISV remit (Envío por parte del ISV).

* En países de "Envío de Microsoft", Microsoft recopila impuestos de clientes y paga impuestos (mandatos) toohello gobierno.
* En "ISV remitir" países, asociados son responsables de recopilar a los clientes de impuestos y pagar los impuestos toohello gobierno. Si decide toosell en países "ISV remitir", debe tener toocalculate de capacidad de Hola y pagar los impuestos en países de Hola que seleccione.

> [!NOTE]
> El SKU no estará disponible en los países de Hola a menos que establezca su plan de tarifa en hello [portal de publicación](https://publish.windowsazure.com). Instrucciones tooget conjunto Hola precios de cada hora y BYOL SKU se indica a continuación.
> 
> 

### <a name="211-how-toosetup-hourly-pricing-model-for-a-sku"></a>2.1.1 cómo toosetup precio por hora de modelo de una SKU
Siga los pasos de hello indicados a continuación toosetup precio por hora de modelo de una SKU:

1. Inicio de sesión toohello [portal de publicación](https://publish.windowsazure.com).
2. Navegue toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En hello izquierdo al lado del menú, haga clic en hello **SKU** ficha.
4. Asegúrese de que Hola que SKU se marca como "Modelo de facturación por hora". Si no es así, a continuación, haga clic en hello **editar** modelo de facturación de botón toorevert Hola. Se mostrará una ventana. Desactive la casilla de verificación de hello 'licencias y facturación se realiza externamente de Azure (también conocido como aportar su propia licencia)' y guardar los cambios de Hola.
5. Si desea tooenable gratuita para 30days primera Hola de implementación de SKU, a continuación, seleccione la opción de Hola "Un mes" for Hola pregunta "es una prueba gratuita disponible?" En caso contrario, seleccione opción de hello "No prueba". Seguidamente, siga los pasos de hello indicados a continuación.
6. En hello izquierdo al lado del menú, haga clic en hello **precios** ficha.
7. Seleccione la región base.
   
   ![dibujo](media/marketplace-publishing-push-to-staging/img2.1.1_07.png)
8. Establecer los precios de Hola para todos los núcleos. **Debe proporcionar el precio para todos los núcleos de Hola de una SKU incluso si no es compatible con el SKU.**
   
    ![dibujo](media/marketplace-publishing-push-to-staging/img2.1.1_08.png)
9. Establecer los precios de Hola para hello otras regiones manualmente o puede usar hello AUTOPRICE Asistente tooset Hola precios de otras regiones en función de la región de base de Hola. toouse hello AUTOPRICE asistente, haga clic en el botón de hello **AUTOPRICE otros mercados basándose en los precios en UNITED STATES.** **Nota:** etiqueta del botón Hola puede ser diferente según la región de Hola que ha seleccionado. Ya que hemos seleccionado Estados Unidos durante la creación de este documento, por lo que botón Hola se etiqueta como "Automático price otros mercados en función de los precios en Estados Unidos" en la siguiente captura de pantalla de Hola.
   
   ![dibujo](media/marketplace-publishing-push-to-staging/img2.1.1_09.png)
10. se abrirá el Asistente de precios de Hello automáticamente. primera página de Hello muestra la selección de Hola de mercado base. Asegúrese de la sección y mover la página siguiente toohello haciendo clic en el botón de "->" Hola.
    
    ![dibujo](media/marketplace-publishing-push-to-staging/img2.1.1_10.png)
11. Opción para seleccionar los planes y los núcleos de Hola se mostrará en la página de hello 2. Seleccione planes de hello deseado y haga clic en "->" botón. Haga clic en hello **Alternar todas** tooselect botón Hola a todos **planes de servicio** y **metros** o pueda comprobar manualmente las casillas de verificación de Hola. **Debe proporcionar el precio para todos los núcleos de Hola de una SKU incluso si no es compatible con el SKU.** Por lo tanto, asegúrese de que se seleccionan todos los tamaños de núcleo de Hola.
    
    ![dibujo](media/marketplace-publishing-push-to-staging/img2.1.1_11.png)
12. Página 3 muestra hello mercados o regiones. Haga clic en hello **Alternar todas** botón tooselect todas las regiones o manualmente las casillas de Hola de región. Haga clic en hello "->" página siguiente del botón toomove toohello. **Nota** : Los países en los que Microsoft se encarga del pago de impuestos se indican con un icono similar a una casa. Para obtener más información, consulte toohello sección "Ventas para" países de hello SKU de esta página.
    
    ![dibujo](media/marketplace-publishing-push-to-staging/img2.1.1_12.png)
13. Página 4 muestra las tasas de cambio de Hola. Haga clic en hello finalizar pasos de botón toocomplete Hola.

### <a name="212-how-toosetup-byol-pricing-model-for-a-sku"></a>2.1.2 cómo modelo de precios de BYOL toosetup para una SKU
Siga los pasos de hello indica a continuación de modelo de precios toosetup BYOL para una SKU:

1. Inicio de sesión toohello [portal de publicación](https://publish.windowsazure.com).
2. Navegue toohello **máquinas virtuales** pestaña y seleccione su oferta.
3. En hello izquierdo al lado del menú, haga clic en hello **SKU** ficha.
4. Asegúrese de que Hola que SKU se marca como "Aporte su propia licencia SKU". Si no es así, a continuación, haga clic en Hola Hola del toorevert del botón de Editar modelo de facturación. Se mostrará una ventana. Activar casilla de verificación de hello 'licencias y facturación se realiza externamente de Azure (también conocido como aportar su propia licencia)' y guarde los cambios de Hola.
   
   ![dibujo](media/marketplace-publishing-push-to-staging/img2.1.2_04.png)
5. En hello izquierdo al lado del menú, haga clic en hello **precios** ficha.
6. Seleccione su región base y asegúrese de Hola SKU disponible en la región de hello activando la casilla de hello contra Hola SKU en sección Hola disponibilidad de SKU de EXTERNALLY-LICENSED (BYOL) (consulte la siguiente captura de pantalla de hello).
   
   ![dibujo](media/marketplace-publishing-push-to-staging/img2.1.2_06.png)
7. Hacer Hola SKU estén disponibles en hello otras regiones manualmente o puede usar el Asistente de hello AUTOPRICE para este propósito. Consulte toohello puntos #9 demasiado #13 (que explica el uso de saludo del Asistente para AUTOPRICE de Hola) en la sección de hello **"2.1.1 cómo toosetup precio por hora de modelo de una SKU"** de esta página.

### <a name="22-set-your-developer-service-prices"></a>2.2. Establecer precios de servicio para desarrolladores
Los planes pueden ser cualquier combinación de base + consumo, donde base es precio mensual de Hola y por encima del límite es precio de pago por uso de Hola. (Vea a continuación para obtener más información).

**Ejemplo:** oferta de servicio de desarrolladores de Contoso

| Plan | Precio | Incluye | Ruta de migración |
| --- | --- | --- | --- |
| Gratuito |0 $/mes |Funcionalidad básica |Puede migrar tooany otro plan |
| Bronze |10 $/mes |La funcionalidad básica y una cuota de 1.000 de la característica X. |Puede migrar tooBronze +, plata y oro planes |
| Bronze Plus |Período de evaluación gratuita: 0 $/mes + 0 $/meter01 |La funcionalidad básica y una cuota de 10.000 característica X.  Una vez que se usa la cuota de la función X, el cliente de hello puede pagar por cada uso a través de meter01. |Puede migrar planes de tooSilver signos más y Gold |
| Bronze Plus |Periodo pago (también conocido como "caducidad de evaluación gratuita"): 10 $/mes + 0,05 $/meter01. |La funcionalidad básica y una cuota de 10.000 característica X.  Una vez que se usa la cuota de la función X, el cliente de hello puede pagar por cada uso a través de meter01. |Puede migrar planes de tooSilver signos más y Gold |
| Silver |$ 0,15/meter01 |Hola cliente puede pagar por cada uso a través de meter01, que es para característica X. |Puede migrar tooBronze y planes de oro |
| Silver Plus |20 $/mes + 0,15 $/meter01 + 0,01 dólares/meter02 |La funcionalidad básica y una cuota de 10.000 de característica X y 100 de característica Y.  Una vez que se usa la cuota de característica X Hola, cliente hello puede pagar por cada uso a través de meter01.  Una vez que se usa la cuota de característica Y Hola, cliente hello puede pagar por cada uso a través de meter02. |Puede migrar planes de tooBronze signos más y Gold |
| Gold |1.000 $/mes |Cuota de 10.000 de la característica X, 1.000 de la característica Y e ilimitada de la característica Z. |Puede migrar planes de tooall salvo libre |

## <a name="step-3-provide-support-information"></a>Paso 3: Especificación de información de soporte técnico
detalles de contacto de Hola se utilizan para la comunicación interna entre los socios de Hola y Microsoft solo. dirección URL de soporte técnico de Hello será los clientes finales de toohello disponible.

1. Vaya toohello **compatibilidad** encabezado en hello parte izquierda de portal de publicación de Hola.
2. Escriba la información de **Contacto de ingeniería**.
3. Escriba la información de **Asistencia al cliente**. Si solo proporciona soporte técnico por correo electrónico, escriba un número de teléfono ficticio, así se utilizará su dirección de correo electrónico.
4. Escriba la dirección URL de soporte técnico de Hola.

## <a name="step-4-choose-azure-marketplace-categories"></a>Paso 4: Elección de categorías de Azure Marketplace
Hola **categorías** ficha proporciona una matriz de las selecciones. Su oferta puede estar en estas, y puede seleccionar las categorías de toofive.

## <a name="how-your-marketing-will-appear"></a>Apariencia del marketing
A continuación se muestra una vista detallada de cómo se utiliza la información de marketing de oferta de hello en hello [sitio Web de Azure Marketplace](https://azure.microsoft.com/marketplace/) y Hola [portal de Azure](https://portal.azure.com).

### <a name="azure-marketplace-website"></a>Sitio web de Azure Marketplace
![dibujo](media/marketplace-publishing-push-to-staging/acom-catalog-01.png)

![dibujo](media/marketplace-publishing-push-to-staging/acom-catalog-02.png)

*Listado de ofertas en el sitio Web de Azure Marketplace de Hola*

![dibujo](media/marketplace-publishing-push-to-staging/acom-listing-details-01.png)

*Detalles de la descripción de la oferta en el sitio Web de Azure Marketplace de Hola*

![dibujo](media/marketplace-publishing-push-to-staging/acom-listing-details-02.png)

*Detalles de precios en el sitio Web de Azure Marketplace de Hola de descripción de la oferta*

### <a name="azure-portal"></a>Portal de Azure
![dibujo](media/marketplace-publishing-push-to-staging/azureportal-galleryblade-01.png)

*Lista de ofertas en hello Portal de Azure*

![dibujo](media/marketplace-publishing-push-to-staging/azureportal-galleryblade-02.png)

*Detalles de la descripción de la oferta en hello portal de Azure*

## <a name="next-steps"></a>Pasos siguientes
Ahora que el contenido de Marketplace está cargado, avanzamos a la prueba de la oferta en ensayo. Sin embargo, debe seleccionar tipo de oferta adecuada de Hola de hello lista, tal y como pasos varían según el tipo de oferta.

* [Prueba de la oferta de máquina virtual en el entorno de ensayo](marketplace-publishing-vm-image-test-in-staging.md)
* [Prueba de la oferta de plantilla de solución en el entorno de ensayo](marketplace-publishing-solution-template-test-in-staging.md)

## <a name="see-also"></a>Otras referencias
* [Introducción: cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md)

[img-map-acom]:media/marketplace-publishing-push-to-staging/pubportal-mapping-acom.jpg
[img-map-portal]:media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg
[img-map-link]:media/marketplace-publishing-push-to-staging/marketing-content-guide-links.jpg
[img-map-logo]:media/marketplace-publishing-push-to-staging/marketing-content-guide-logos.jpg
[img-map-title]:media/marketplace-publishing-push-to-staging/marketing-content-guide-publisher-offer.png

[link-pubportal]:https://publish.windowsazure.com
[link-push-to-production]:marketplace-publishing-push-to-production.md
