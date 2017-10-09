---
título: aaa "lección tutorial de Analysis Services de Azure 13: implementar | Descripción de Microsoft Docs": describe cómo del proyecto tutorial de hello toodeploy tooAzure Analysis Services.
servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 17/07/2017 ms.author: owend
---
# <a name="lesson-13-deploy"></a>Lección 13: Implementación

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, configurará propiedades de implementación; especificar un tooand de toodeploy de servidor de Analysis Services de Azure un nombre para el modelo de Hola. A continuación, implemente instancia toothat de hello modelo. Después de implementa el modelo, los usuarios pueden conectarse tooit mediante el uso de una aplicación de cliente de informes. más información, consulte toolearn [implementar tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Estimado toocomplete de tiempo en esta lección: **5 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 12: analizar en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Debe tener [permisos de administrador](../analysis-services-server-admins.md) en hello remoto Analysis Services server toodeploy en orden tooit.  

> [!IMPORTANT]  
> Si instaló la base de datos de ejemplo de Hola AdventureWorksDW2014 en un servidor local de SQL, y va a implementar el servidor de Analysis Services de Azure de modelo tooan, un [puerta de enlace de datos local](../analysis-services-gateway.md) es necesario.
  
## <a name="deploy-hello-model"></a>Implementar el modelo de Hola  
  
#### <a name="tooconfigure-deployment-properties"></a>propiedades de implementación de tooconfigure  

  
1.  En **el Explorador de soluciones**, contextual hello **AW Internet Sales** del proyecto y, a continuación, haga clic en **propiedades**.  
  
2.  Hola **páginas de propiedades de ventas de Internet de AW** cuadro de diálogo **el servidor de implementación**, Hola **Server** propiedad, escriba servidor completo de Hola.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  Hola **base de datos** propiedad, escriba **Adventure Works Internet Sales**.  
  
4.  Hola **nombre del modelo** propiedad, escriba **Adventure Works Internet Sales Model**.  
  
5.  Compruebe sus selecciones y, a continuación, haga clic en **Aceptar**.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>Hola toodeploy Adventure Works Internet Sales
  
1.  En **el Explorador de soluciones**, contextual hello **AW Internet Sales** proyecto > **generar**.  

2.  Menú contextual hello **AW Internet Sales** proyecto > **implementar**.

    Al implementar tooAzure Analysis Services, puede ser solicitada tooenter su cuenta. Escriba su cuenta profesional y la contraseña, por ejemplo nancy@adventureworks.com. Esta cuenta debe ser de administradores en el servidor de Hola.
  
    cuadro de diálogo implementar Hola aparece y muestra el estado de implementación de Hola de metadatos de Hola y cada tabla incluida en el modelo de Hola.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. Cuando la implementación finalice correctamente, siga adelante y haga clic en **Cerrar**.  
  
## <a name="conclusion"></a>Conclusión  
¡Enhorabuena! Ha terminado de crear e implementar el primer modelo tabular de Analysis Services. Este tutorial ha ayudado a ayudará a completar las tareas más comunes de hello en la creación de un modelo tabular. Ahora que se implementa el modelo de ventas por Internet de Adventure Works, puede utilizar el modelo de SQL Server Management Studio toomanage Hola; crear secuencias de comandos de proceso y un plan de copia de seguridad. Los usuarios pueden conectarse ahora también modelo toohello mediante una aplicación de cliente de informes como Microsoft Excel o Power BI.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Pasos siguientes
[Conexión con Power BI Desktop](../analysis-services-connect-pbi.md)   
[Lección complementaria: Seguridad dinámica](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Lección complementaria: Filas de detalles](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Lección complementaria: Jerarquías desiguales](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
