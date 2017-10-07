---
title: "aaaAuthor los módulos de R personalizado en aprendizaje automático de Azure | Documentos de Microsoft"
description: "Inicio rápido para la creación de módulos R personalizados en Aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>Creación de módulos R personalizados en Aprendizaje automático de Azure
Este tema se describe cómo tooauthor e implementar un módulo personalizado de R en aprendizaje automático de Azure. Explica qué son los módulos de R personalizados y qué archivos son toodefine usado ellos. Ilustra cómo tooconstruct Hola archivos que definen un módulo y cómo tooregister Hola módulo para la implementación en un área de trabajo de aprendizaje automático. Hello elementos y atributos que se utilizan en la definición de Hola de módulo personalizado de hello son, a continuación, se describe con más detalle. Cómo también se describe la funcionalidad auxiliar toouse y archivos y varias salidas. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>¿Qué es un módulo R personalizado?
A **módulo personalizado** es un módulo definido por el usuario que se puede carga el área de trabajo de tooyour y se ejecuta como parte de un experimento de aprendizaje automático de Azure. Un **módulo de R personalizado** es un módulo personalizado que ejecuta una función de R definida por el usuario. **R** es un lenguaje de programación de computación estadística y gráficos utilizado ampliamente por científicos estadísticos y de datos para implementar algoritmos. Actualmente, R es admitido en módulos personalizados, pero la compatibilidad para idiomas adicionales está programada para futuras versiones de idioma solo Hola.

Los módulos personalizados tienen **estatus** aprendizaje automático de Azure en sentido Hola que puede usarse como cualquier otro módulo. Pueden ejecutarse con otros módulos e incluirse en experimentos publicados o visualizaciones. Tiene control sobre el algoritmo de hello implementado por el módulo de hello, Hola toobe de puertos de entrada y salida que se usa, Hola parámetros de modelado y otros distintos comportamientos en tiempo de ejecución. Un experimento contiene módulos personalizados también se puede publicar en hello Cortana Intelligence Galería para compartir fácilmente.

## <a name="files-in-a-custom-r-module"></a>Archivos de un módulo R personalizado
Un módulo R personalizado se define mediante un archivo .zip que contiene, como mínimo, dos archivos:

* A **archivo de código fuente** que implementa la función de hello R expuesta por el módulo de Hola
* Un **archivo de definición XML** que describe la interfaz de módulo personalizado de Hola

Archivos auxiliares adicionales también pueden incluirse en el archivo .zip de Hola que proporciona la funcionalidad que puede tener acceso desde el módulo personalizado de Hola. Esta opción se describe en hello **argumentos** forma parte de la sección de referencia de hello **elementos en el archivo de definición XML de hello** siguiente ejemplo de Hola inicio rápido.

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>Ejemplo de inicio rápido: definir, empaquetar y registrar un módulo R personalizado
Este ejemplo ilustra cómo tooconstruct Hola archivos requeridos por un módulo personalizado de R, empaquetarlos en un archivo zip y, a continuación, un módulo de hello registrar en el área de trabajo de aprendizaje automático. Hello archivos de ejemplo y el paquete de ejemplo zip pueden descargarse desde [CustomAddRows.zip Descargar archivo](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).

## <a name="hello-source-file"></a>archivo de código fuente de Hola
Considere la posibilidad de ejemplo de Hola de un **personalizado agregar filas** módulo que modifica la implementación estándar de Hola de hello **agregar filas** módulo usa tooconcatenate filas (observaciones) de dos conjuntos de datos (tramas de datos). Hola estándar **agregar filas** módulo anexa filas de hello del segundo conjunto de datos de entrada toohello final de Hola de hello primera entrada conjunto de datos mediante hello `rbind` algoritmo. Hola personalizado `CustomAddRows` función acepta dos conjuntos de datos de forma similar, pero también acepta un parámetro booleano intercambio como una entrada adicional. Si el parámetro de intercambio de Hola se establece demasiado**FALSE**, devuelve Hola el mismo conjunto de datos como Hola implementación estándar. Sin embargo, si el parámetro de intercambio de hello es **TRUE**, función hello anexa filas del primer conjunto de datos de entrada toohello end de hello segundo conjunto de datos en su lugar. archivo CustomAddRows.R Hello que contiene la implementación de Hola de hello R `CustomAddRows` función expuesta por hello **personalizado agregar filas** módulo tiene Hola siguiente código de R.

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a>archivo de definición XML de Hola
tooexpose esto `CustomAddRows` función como un módulo de aprendizaje automático de Azure, un archivo de definición XML debe crearse toospecify cómo Hola **personalizado agregar filas** módulo debe aspecto y comportamiento. 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


Es toonote crítico que Hola valo hello **Id. de** atributos de hello **entrada** y **Arg** elementos en el archivo XML de hello deben coincidir con los nombres de parámetro de función de Hola de hello R código de archivo de hello CustomAddRows.R exactamente: (*dataset1*, *dataset2*, y *intercambio* en el ejemplo de Hola). Hola de forma similar, el valor de hello **entryPoint** atributo de hello **lenguaje** elemento debe coincidir exactamente con hello nombre de función de hello en el script de Hola R: (*CustomAddRows* en el ejemplo de Hola). 

En cambio, Hola **Id. de** atributo para hello **salida** elemento no corresponde tooany variables de script de Hola R. Cuando se requiere más de un resultado, simplemente devuelven una lista de función hello R con resultados colocados *Hola mismo orden* como **salidas** elementos se declaran en el archivo XML de hello.

### <a name="package-and-register-hello-module"></a>Módulo de Hola de paquete y registro
Guardar estos dos archivos como *CustomAddRows.R* y *CustomAddRows.xml* y, a continuación, zip Hola dos archivos juntos en un *CustomAddRows.zip* archivo.

tooregister en el área de trabajo de aprendizaje automático, área de trabajo vaya tooyour Hola estudio de aprendizaje automático, haga clic en hello **+ nuevo** situado en la parte inferior de Hola y elija **módulo -> de ZIP del paquete** tooupload Hola nueva **personalizado agregar filas** módulo.

![Cargar archivo zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

Hola **personalizado agregar filas** módulo ahora está listo toobe acceso a sus experimentos de aprendizaje automático.

## <a name="elements-in-hello-xml-definition-file"></a>Elementos de archivo de definición XML de Hola
### <a name="module-elements"></a>Elementos Module
Hola **módulo** elemento es toodefine usado un módulo personalizado en el archivo XML de hello. Se pueden definir varios módulos en un archivo XML mediante el uso de varios elementos **Module** . Cada uno de los módulos del área de trabajo debe tener un nombre único. Registrar un módulo personalizado con el mismo nombre como un módulo personalizado existente de Hola y reemplaza módulo existente Hola con hello uno nuevo. Sin embargo, los módulos personalizados se pueden registrar con el mismo nombre como un módulo de aprendizaje automático de Azure existente de Hola. Si es así, aparecen en hello **personalizado** categoría de la paleta de módulo de Hola.

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


Dentro de hello **módulo** elemento, puede especificar dos elementos opcionales adicionales:

* un **propietario** elemento incrustado en el módulo de Hola  
* un **descripción** elemento que contiene el texto que se muestra en la Ayuda rápida para el módulo de Hola y cuando mantenga el mouse sobre módulo Hola Hola interfaz de usuario de aprendizaje de máquina.

Reglas para los límites de caracteres en elementos de módulo de hello:

* Hola valo hello **nombre** atributo Hola **módulo** elemento no debe superar los 64 caracteres de longitud. 
* Hola contenido de hello **descripción** elemento no debe superar los 128 caracteres de longitud.
* Hola contenido de hello **propietario** elemento no debe superar los 32 caracteres de longitud.

Resultados de un módulo pueden ser deterministas o nondeterministic.* * de forma predeterminada, todos los módulos se consideran toobe determinista. Es decir, dado un conjunto de parámetros de entrada y los datos que no cambian, módulo de hello debería devolver Hola mismo da como resultado eacRAND o una vez functionh que se ejecuta. Dado este comportamiento, estudio de aprendizaje automático de Azure solo vuelve a ejecutar los módulos que se marca como determinista si un parámetro o datos de entrada de hello ha cambiado. Devolver los resultados de hello en caché, también proporciona mucho una ejecución más rápida de experimentos.

Hay funciones que no son deterministas, como RAND o una función que devuelve Hola fecha y hora actuales. Si el módulo usa una función no determinista, puede especificar ese módulo hello no es determinista por establecer Hola opcional **isDeterministic** atributo demasiado**FALSE**. Esto garantiza que ese módulo Hola se vuelve a ejecutar siempre que se ejecute el experimento de hello, incluso si hello módulo parámetros de entrada y no han cambiado. 

### <a name="language-definition"></a>Definición de lenguaje
Hola **lenguaje** element en el archivo de definición XML es el idioma de módulo personalizado de Hola de toospecify usado. Actualmente, R es Hola solo admite el idioma. Hola valo hello **sourceFile** atributo debe ser el nombre de hello del archivo de hello R que contiene Hola función toocall cuando se ejecuta el módulo de Hola. Este archivo debe ser parte del paquete comprimido de Hola. Hola valo hello **entryPoint** atributo es Hola nombre de función hello que se llama y debe coincidir con una función válida que se definen en el archivo de código fuente de Hola.

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>Puertos
Hello puertos de entrada y salidos para un módulo personalizado especificados en los elementos secundarios de hello **puertos** sección del archivo de definición XML de Hola. orden de Hola de estos elementos determina Hola diseño experimentado (UX) por los usuarios. primer elemento secundario de Hello **entrada** o **salida** enumerados en hello **puertos** elemento del archivo XML de Hola se convierte en el puerto de entrada del extremo izquierdo de Hola Hola UX. de aprendizaje de máquina
Cada entrada y puerto de salida puede tener una función opcional **descripción** elemento secundario que especifica el texto hello se muestra cuando coloques el cursor del mouse de hello en el puerto de Hola Hola interfaz de usuario de aprendizaje de máquina.

**Reglas de puertos**:

* El número máximo de **puertos de entrada y salida** es 8 para cada uno.

### <a name="input-elements"></a>Elementos de entrada
Puertos de entrada permiten área de trabajo y función de toopass datos tooyour R. Hola **tipos de datos** que son compatibles con puertos de entrada son los siguientes: 

**DataTable:** se pasa este tipo de función tooyour R como un data.frame. De hecho, los tipos (por ejemplo, archivos CSV o archivos ARFF) que son compatibles con el aprendizaje automático y que son compatibles con **DataTable** son data.frame tooa convertido automáticamente. 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

Hola **identificador** atributo asociado con cada uno de ellos **DataTable** puerto de entrada debe tener un valor único y este valor debe coincidir con el parámetro en la función de R con nombre correspondiente.
Opcional **DataTable** puertos que no se pasan como entrada en un experimento tienen valor hello **NULL** función pasado toohello R y los puertos de zip opcional se omiten si Hola entrada no está conectado. Hola **isOptional** atributo es opcional para ambos hello **DataTable** y **código postal** tipos y *false* de forma predeterminada.

**Zip:** los módulos personalizados pueden aceptar un archivo .zip como entrada. Esta entrada se desempaqueta en el directorio de trabajo de hello R de la función

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

Para los módulos de R personalizados, Id. de Hola para un puerto Zip no tiene toomatch los parámetros de función hello R. Esto es porque el archivo zip de hello es automáticamente extraídos toohello R directorio de trabajo.

**Reglas de entrada:**

* Hola valo hello **Id. de** atributo de hello **entrada** elemento debe ser un nombre de variable válido de R.
* Hola valo hello **Id. de** atributo de hello **entrada** elemento no debe superar los 64 caracteres.
* Hola valo hello **nombre** atributo de hello **entrada** elemento no debe superar los 64 caracteres.
* Hola contenido de hello **descripción** elemento no debe tener más de 128 caracteres
* Hola valo hello **tipo** atributo de hello **entrada** el elemento debe estar *código postal* o *DataTable*.
* Hola valo hello **isOptional** atributo de hello **entrada** elemento no es necesario (y es *false* de forma predeterminada cuando no se especifica); pero si se especifica, debe ser *true* o *false*.

### <a name="output-elements"></a>Elementos de salida
**Puertos de salida estándar:** puertos de salida son asignadas toohello valores devueltos de la función de R, que, a continuación, se puede usar módulos posteriores. *DataTable* Hola tipo de puerto de salida estándar sólo admitidos actualmente. (Próximamente se incluirá compatibilidad con *Learners* y *Transforms*). Una salida de *DataTable* se define como:

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

Los resultados en los módulos de R personalizados, Hola valo hello **identificador** atributo no tiene toocorrespond con nada en el script de Hola R, pero debe ser único. Para una salida de módulo único, valor devuelto de Hola de función hello R debe ser un *data.frame*. En Ordenar toooutput más de un objeto de un tipo de datos admitidos, puertos de salida correspondiente Hola necesitan toobe especificado en el archivo de definición XML de Hola y Hola objetos necesitan ser toobe devuelve como una lista. objetos de salida de Hello asigna puertos toooutput desde tooright izquierdo, reflejar el orden de hello en el que se colocan los objetos de hello en hello devuelve la lista.

Por ejemplo, si desea hello toomodify **personalizado agregar filas** toooutput módulo Hola originales dos conjuntos de datos, *dataset1* y *dataset2*, además unido toohello nueva conjunto de datos, *conjunto de datos*, (en un orden, de izquierda tooright, como: *conjunto de datos*, *dataset1*, *dataset2*), a continuación, defina Hola puertos en el archivo de hello CustomAddRows.xml de salida como se indica a continuación:

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


Y devuelve la lista de Hola de objetos en una lista en orden correcto de hello en 'CustomAddRows.R':

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**Salida de visualización:** también puede especificar un puerto de salida de tipo *visualización*, que muestra información sobre Hola de salida de consola y dispositivo de gráficos de hello R. Este puerto no es parte de la salida de función hello R y no interfiere con el orden de Hola de hello otro tipos de puerto de salida. Agregar una visualización puerto toohello módulos personalizados de tooadd una **salida** elemento con un valor de *visualización* para su **tipo** atributo:

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**Reglas de salida:**

* Hola valo hello **identificador** atributo de hello **salida** elemento debe ser un nombre de variable válido de R.
* Hola valo hello **identificador** atributo de hello **salida** elemento no debe superar los 32 caracteres.
* Hola valo hello **nombre** atributo de hello **salida** elemento no debe superar los 64 caracteres.
* Hola valo hello **tipo** atributo de hello **salida** el elemento debe estar *visualización*.

### <a name="arguments"></a>Argumentos
Datos adicionales se pueden pasar toohello R función a través de los parámetros del módulo que se definen en hello **argumentos** elemento. Estos parámetros aparecen en panel de propiedades más a la derecha de Hola de interfaz de usuario de aprendizaje de máquina de hello cuando está seleccionado el módulo de Hola. Los argumentos pueden ser cualquiera de los tipos compatibles de Hola o puede crear una enumeración personalizada cuando sea necesario. Toohello similar **puertos** elementos, **argumentos** elementos pueden tener una función opcional **descripción** elemento que especifica el texto hello que aparece al colocar el puntero del mouse Hola nombre de parámetro de Hola.
Se pueden agregar propiedades opcionales para un módulo, por ejemplo, defaultValue, minValue y maxValue tooany argumento como atributos tooa **propiedades** elemento. Propiedades válidas para hello **propiedades** elemento dependen de tipo de argumento de Hola y se describen con hello admite tipos de argumento en la sección siguiente Hola. Argumentos con hello **isOptional** propiedad establecida demasiado**"true"** no requieren Hola usuario tooenter un valor. Si no se proporciona un valor toohello argumento, argumento de hello no se pasa toohello función de punto de entrada. Argumentos de función de punto de entrada de Hola que son toobe necesidad opcional controle explícitamente la función hello, por ejemplo, asigna un valor predeterminado es NULL en la definición de función de punto de entrada de Hola. Un argumento opcional solo aplicará Hola otras restricciones de argumento, es decir, min o max, si un valor proporcionado por el usuario de Hola.
Al igual que con las entradas y salidas, es fundamental que cada uno de los parámetros de hello tiene valores de identificador único asociados a ellos. En nuestro tutorial era ejemplo Hola asociados parámetro/id *intercambio*.

### <a name="arg-element"></a>Elemento Arg
Un parámetro de módulo se define utilizando hello **Arg** elemento secundario de hello **argumentos** sección del archivo de definición XML de Hola. Al igual que con los elementos secundarios Hola Hola **puertos** sección, Hola ordenar los parámetros en hello **argumentos** sección define el diseño de hello en hello UX. Hello parámetros aparecen de arriba hacia abajo en hello interfaz de usuario en el mismo orden en que se definen de hello en el archivo XML de hello. a continuación se enumeran los tipos de Hello admitidos por aprendizaje automático para los parámetros. 

**int** : parámetro de tipo entero (32 bits).

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *Propiedades opcionales*: **min**, **max**, **default** e **isOptional**

**double** : parámetro de tipo doble.

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *Propiedades opcionales*: **min**, **max**, **default** e **isOptional**

**bool** : parámetro booleano que se representa mediante una casilla en la experiencia de usuario.

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *Propiedades opcionales*: **default** : false si no se ha establecido

**string**: una cadena estándar.

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *Propiedades opcionales*: **default** e **isOptional**

**ColumnPicker**: parámetro de selección de columnas. Este tipo se representa en hello UX como un selector de columnas. Hola **propiedad** elemento es el Id. de Hola de toospecify aquí usado del puerto de Hola desde el que se seleccionan las columnas, donde el tipo de puerto de destino de hello debe ser de *DataTable*. resultado de Hello de selección de la columna de Hola se pasa toohello R función como una lista de cadenas que contienen nombres de columna de hello seleccionado. 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *Propiedades necesarias*: **portId** -coincidencias Hola Id. de un elemento de entrada con tipo *DataTable*.
* *Propiedades opcionales*:
  
  * **allowedTypes** -tipos de las columnas de hello filtros desde la que puede elegir. Los valores válidos son: 
    
    * Numeric
    * Booleano
    * Categorías
    * string
    * Etiqueta
    * Característica
    * Score
    * Todo
  * **valor predeterminado** -selecciones predeterminadas válido para el selector de columna Hola incluyen: 
    
    * None
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * Todo

**Desplegable**: lista (desplegable) especificada por el usuario que se muestra. elementos de lista desplegable de Hola se especifican en hello **propiedades** elemento mediante un **elemento** elemento. Hola **identificador** para cada **elemento** debe ser único y una variable de R válida. Hola valo hello **nombre** de un **elemento** actúa como texto hello que se ve y valor de Hola que se pasa la función toohello R.

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *Propiedades opcionales*:
  * **valor predeterminado** : hello valor de la propiedad predeterminada de hello debe corresponder con un valor de identificador de uno de hello **elemento** elementos.

### <a name="auxiliary-files"></a>Archivos auxiliares
Cualquier archivo que se coloca en el archivo ZIP de módulo personalizado es continuo toobe disponible para su uso durante el tiempo de ejecución. Se conservarán todas las estructuras de directorios presentes. Esto significa que funciona de origen de archivo Hola mismo localmente y en la ejecución de aprendizaje automático de Azure. 

> [!NOTE]
> Tenga en cuenta que todos los archivos extraídos too'src' directory para que todas las rutas de acceso deben tener ' src /' prefijo.
> 
> 

Por ejemplo, suponga que desee tooremove las filas con NAs de conjunto de datos de Hola y quita todas las filas duplicadas, antes de generar en CustomAddRows y ya ha escrito una función de R que lo hace en un archivo RemoveDupNARows.R:

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
Puede obtener el archivo auxiliar RemoveDupNARows.R Hola Hola CustomAddRows función:

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

A continuación, cargue un archivo zip que contenga "myAddRows.R", "myAddRows.xml" y "removeDupNARows.R" como módulo de R personalizado.

## <a name="execution-environment"></a>Entorno de ejecución
entorno de ejecución de Hola para script de Hola R usa Hola misma versión de R que hello **ejecutar Script de R** módulo y puede usar Hola mismo predeterminado paquetes. También puede agregar más módulo personalizado de R paquetes tooyour incluyéndolos en el paquete comprimido de módulo personalizado de Hola. Solo tiene que cargarlos en el script de R como lo haría en su propio entorno de R. 

**Limitaciones del entorno de ejecución de hello** incluyen:

* Sistema de archivos no persistentes: no se conservan los archivos escritos cuando se ejecuta el módulo personalizado de Hola durante varias ejecuciones de hello mismo módulo.
* Sin acceso de red

