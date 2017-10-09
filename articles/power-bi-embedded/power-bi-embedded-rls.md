---
title: seguridad de nivel de aaaRow con Power BI Embedded
description: "Más información sobre la seguridad de nivel de fila con Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Seguridad de nivel de fila con Power BI Embedded

Seguridad de nivel de fila (RLS) puede ser datos de tooparticular de acceso de usuario de toorestrict utilizados dentro de un informe o un conjunto de datos, permitiendo varias toouse distintos usuarios Hola mismo informe al ver todos los datos diferentes. Power BI Embedded ahora admite conjuntos de datos configurados con RLS.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

En orden tootake aprovechar RLS, es importante que comprenda los conceptos principales tres; Los usuarios, Roles y reglas. Profundicemos en cada uno de ellos:

**Los usuarios** : estos son los usuarios finales real de hello ver informes. En Power BI Embedded, los usuarios se identifican por la propiedad de nombre de usuario de hello en un Token de aplicación.

**Roles** : los usuarios pertenecen tooroles. Un rol es un contenedor de reglas y se puede adoptar un nombre como "Administrador de ventas" o "Representante de ventas". En Power BI Embedded, los usuarios se identifican por la propiedad de roles de hello en un Token de aplicación.

**Reglas de** : Roles tienen reglas, y dichas reglas son filtros real Hola va toobe aplica toohello datos. Esto podría ser tan simple como "Country = USA" o algo mucho más dinámico.

### <a name="example"></a>Ejemplo

Para el resto de Hola de este artículo, le presentaremos un ejemplo de creación de RLS y, a continuación, consumir dentro de una aplicación incrustada. El ejemplo usa hello [ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547) archivo PBIX.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

Nuestro ejemplo de análisis de minoristas muestra las ventas de todos los almacenes de hello en una cadena de venta específico. Sin RLS, con independencia de qué distrito administrador inicia sesión y vistas hello informe, verá Hola los mismos datos. Directivos determinó que cada administrador del distrito solo debe ver hello ventas para los almacenes de hello administran y toodo esto, podemos usar RLS.

RLS se ha creado en Power BI Desktop. Cuando se abren el conjunto de datos de Hola y el informe, podemos cambiar esquema Hola de toodiagram vista toosee:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

A continuación, presentamos unos toonotice de cosas con este esquema:

* Al igual que todas las medidas, **ventas totales**, se almacenan en hello **ventas** tabla de hechos.
* Hay cuatro tablas de dimensiones adicionales relacionadas: **Item**, **Time**, **Store** y **District**.
* las flechas de Hello en las líneas de relación de hello indican qué forma filtros pueden fluir de una tabla tooanother. Por ejemplo, si se coloca un filtro en **tiempo [Date]**, en el esquema actual de hello sólo debería filtrar valores en hello **ventas** tabla. Ninguna otra tabla se vería afectado por este filtro debido a que todos las flechas de hello en la tabla de ventas de punto toohello de líneas de relación de Hola y no inmediatamente.
* Hola **distrito** tabla indica quién es el director de Hola para cada distrito:
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

Basada en este esquema, si se aplica un filtro toohello **administrador del distrito** columna Hola tabla distrito y si ese filtro coincide con usuario Hola Ver informe de hello, ese filtro también filtrará hacia abajo hello **almacén**y **ventas** tooonly tablas muestran datos de ese determinado distrito manager.

Este es el procedimiento:

1. En la pestaña de modelado de hello, haga clic en **administrar funciones**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Cree un nuevo rol denominado **Manager**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. Hola **distrito** tabla escriba Hola siguiente expresión de DAX: **[Administrador del distrito] = USERNAME()**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. toomake seguro Hola reglas funcionan, en hello **modelado** , haga clic en **ver como Roles**y escriba Hola siguiente:  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   Hello informes ahora mostrará datos como si se han iniciado sesión como **Andrew Ma**.

Aplicar filtro hello, Hola hicimos en este caso, se filtrará hacia abajo todos los registros de hello **distrito**, **almacén**, y **ventas** tablas. Sin embargo, debido a la dirección del filtro hello en relaciones de hello entre **ventas** y **tiempo**, **ventas** y **elemento**y **Elemento** y **tiempo** tablas no se filtrarán hacia abajo.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Que puede ser correcto para este requisito, sin embargo, si no queremos administradores toosee elementos para los que no tengan ninguna venta, se puede activar bidireccional filtrado cruzado para hello relación y flujo de hello filtro de seguridad en ambas direcciones. Esto puede hacerse mediante la edición de relación de hello entre **ventas** y **elemento**, similar a la siguiente:

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

Ahora, los filtros también pueden fluir de Hola ventas tabla toohello **elemento** tabla:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Si usa el modo DirectQuery para los datos, necesitará tooenable bidireccional-entre filtrado mediante la selección de estas dos opciones:

1. **Archivo** ->  **Opciones y configuración** -> **Características de vista previa** -> **Enable cross filtering in both directions for DirectQuery** (Habilitar filtrado cruzado en ambas direcciones para DirectQuery).
2. **Archivo** -> **Opciones y configuración** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode** (Permitir medida sin restricciones en el modo DirectQuery).

más información sobre filtrado cruzado bidireccional, descarga hello toolearn [filtrado cruzado bidireccional en SQL Server Analysis Services 2016 y Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) notas del producto.

Esto concluye todo el trabajo de Hola que necesita toobe realiza en Power BI Desktop, pero no hay uno más parte del trabajo que necesita toobe realiza toomake Hola RLS reglas definimos trabajo en Power BI Embedded. Los usuarios se autentican y autorizan mediante la aplicación y los tokens de aplicación son usado toogrant ese usuario acceso tooa Power BI Embedded informe específico. Power BI Embedded no tiene información específica en quién es el usuario. Para toowork RLS, necesitará toopass algún contexto adicional como parte de su token de aplicación:

* **nombre de usuario** (opcional): usar con RLS es una cadena que se puede usar toohelp identificar usuario Hola al aplicar reglas RLS. Consulte el uso de la seguridad de nivel de fila con Power BI Embedded
* **roles** : una cadena que contiene Hola roles tooselect al aplicar las reglas de seguridad de nivel de fila. Si se pasa más de un rol, se deben pasar como una matriz de cadenas.

Crear el token de hello mediante hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) método. Si la propiedad de nombre de usuario de hello está presente, también debe pasar al menos un valor en roles.

Por ejemplo, puede cambiar hello EmbedSample. La línea 55 de DashboardController se puede actualizar desde

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

to

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

token de la aplicación completa de Hello tendrá un aspecto similar al siguiente:

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

Ahora, con todas las piezas de hello juntas, cuando un usuario inicia sesión en nuestra aplicación tooview este informe, solo estarán toosee capaz de datos de Hola que pueden toosee, tal como se define por la seguridad de nivel de fila.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>Otras referencias

[Seguridad de nivel de fila](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)  
¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)

