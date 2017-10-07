---
title: "aaaDesigning aplicaciones altamente disponibles con almacenamiento con redundancia geográfica de Azure con acceso de lectura (RA-GRS) | Documentos de Microsoft"
description: "¿Cómo tooarchitect de almacenamiento de Azure RA-GRS toouse una aplicación de alta disponibilidad flexible suficiente interrupciones toohandle."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>Diseño de aplicaciones de alta disponibilidad mediante RA-GRS

Una característica común de las infraestructuras en la nube es que proporcionan una plataforma de alta disponibilidad para hospedar aplicaciones. Deben tener en cuenta a los desarrolladores de aplicaciones basadas en nube cuidadosamente cómo tooleverage esta plataforma toodeliver aplicaciones de alta disponibilidad tootheir a los usuarios. En este artículo se centra específicamente en cómo los desarrolladores pueden usar hello Azure almacenamiento acceso de lectura almacenamiento con redundancia geográfica (RA-GRS) toomake sus aplicaciones están disponibles.

Existen cuatro opciones de redundancia: LRS (almacenamiento con redundancia local), ZRS (almacenamiento con redundancia de zona), GRS (almacenamiento con redundancia geográfica) y RA-GRS (almacenamiento con redundancia geográfica con acceso de lectura). Vamos a toodiscuss GRS y RA-GRS en este artículo. Con la GRS, tres copias de los datos se mantienen en la región principal de hello seleccionado al configurar la cuenta de almacenamiento de Hola. Se mantienen tres copias adicionales de forma asincrónica en una región secundaria especificada por Azure. RA-GRS es Hola lo mismo que GRS salvo que tienen copia secundaria de toohello de acceso de lectura. Para obtener más información acerca de las opciones de redundancia de almacenamiento de Azure diferentes hello, consulte [replicación de almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy). artículo de replicación de Hello también muestra hello emparejamientos de las regiones principal y secundaria de Hola.

Hay fragmentos de código incluidos en este artículo y un ejemplo completo de vínculo tooa final Hola que puede descargar y ejecutar.

## <a name="key-features-of-ra-grs"></a>Características fundamentales de RA-GRS

Antes de hablar acerca de cómo toouse almacenamiento RA-GRS, tratemos sobre sus propiedades y su comportamiento.

* Almacenamiento de Azure mantiene una copia de solo lectura de datos de Hola que almacena en su región primaria en una región secundaria; tal y como se mencionó anteriormente, el servicio de almacenamiento de Hola determina la ubicación de Hola de región secundaria Hola.

* copia de solo lectura de Hello es [coherente](https://en.wikipedia.org/wiki/Eventual_consistency) con datos de hello en la región principal de Hola.

* Para blobs, tablas y colas, puede consultar la región secundaria de Hola para un *hora de última sincronización* valor que indica cuándo se produjo la última replicación de Hola de región secundaria de hello toohello principal. (esto no se admite para Azure File Storage, que no tiene redundancia RA-GRS en este momento).

* Puede usar Hola biblioteca cliente de almacenamiento toointeract con datos de Hola en cualquier región de hello principal o secundaria. También puede redirigir solicitudes de lectura automáticamente región secundaria toohello si se agota el tiempo de espera de una región principal de toohello de solicitud de lectura.

* Si hay un problema grave que afectan a la accesibilidad de Hola de datos de hello en la región principal de hello, Hola, equipo de Azure puede desencadenar una conmutación geográfica, momento en que las entradas DNS de Hola que señala la región principal toohello serán región secundaria de toopoint modificadas toohello.

* Si se produce una conmutación geográfica, Azure se seleccionar una nueva ubicación secundaria y replicar la ubicación de los datos toothat Hola y luego elija hello tooit de las entradas DNS secundaria. extremo secundario Hola dejará de estar disponible hasta que la cuenta de almacenamiento de hello ha terminado de replicar. Para obtener más información, vea [qué toodo si se produce una interrupción de almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance).

## <a name="application-design-considerations-when-using-ra-grs"></a>Consideraciones sobre el diseño de aplicaciones cuando se usa RA-GRS

Hola principal finalidad de este artículo es tooshow, cómo toodesign una aplicación que va a continuar toofunction (aunque en una capacidad limitada) incluso en caso de hello de un desastre importante en datos principales de hello center. Para ello, haciendo que su transitorio toohandle de aplicación o problemas de ejecución prolongada cambiando tooread de región secundaria Hola mientras hay un problema, y volver al área principal de hello esté disponible de nuevo.

### <a name="using-eventually-consistent-data"></a>Uso de datos con coherencia final

Esta solución propuesta supone que es correcto tooreturn ¿cuál podría ser la aplicación que realiza la llamada de toohello datos obsoletos. Porque los datos secundarios de hello son coherentes, es posible que se escribieron datos de hello toohello principal pero Hola actualización toohello secundaria no había finalizado replicar cuando región principal Hola pasara a ser inaccesible.

Por ejemplo, el cliente puede enviar una actualización que es correcta y, a continuación, podría Bajar Hola principal antes de hello actualización propagado toohello secundaria. En este caso, si el cliente hello después pide datos tooread hello, recibe datos obsoletos de hello en lugar de datos de hello actualizado. Debe decidir si es aceptable y si es así, cómo se un mensaje del cliente de Hola. Podrá ver cómo toocheck Hola última hora de sincronización de datos secundaria de hello más adelante en este artículo toosee si Hola secundario está actualizado.

### <a name="handling-services-separately-or-all-together"></a>Control de servicios por separado o conjuntamente

Aunque no probable, es posible para un servicio toobecome no está disponible mientras hello otros servicios siguen siendo totalmente funcionales. También pueden identificador hello reintentos y el modo de solo lectura para cada servicio por separado (blobs, colas, tablas), o puede controlar reintentos forma genérica para todos los servicios de almacenamiento de hello juntos.

Por ejemplo, si usa las colas y blobs en la aplicación, puede decidir tooput en errores de código independiente toohandle puede intentar de nuevo para cada uno de ellos. A continuación, si obtendrá un reintento de servicio de blob de hello, pero el servicio de cola de hello sigue funcionando, solo una parte de la aplicación que controla blobs Hola se verá afectada. Si decide toohandle servicio de almacenamiento de todos los reintentos genéricamente y un servicio de blob de toohello llamada devuelve un error irreproducible, a continuación, se verá afectados el servicio de blob de solicitudes tooboth Hola y el servicio de cola de Hola.

En última instancia, esto depende en complejidad hello de la aplicación. Puede decidir no errores de hello toohandle por servicio, sino tooredirect las solicitudes para todos los región secundaria de almacenamiento servicios toohello de lectura y ejecutar aplicación hello en modo de solo lectura cuando se detecte un problema con cualquier servicio de almacenamiento en la región principal de Hola.

### <a name="other-considerations"></a>Otras consideraciones

Estos son Hola otras consideraciones, veremos en el resto de Hola de este artículo.

*   Controlar los reintentos de solicitudes de lectura mediante el patrón de disyuntor de Hola

*   Hello última hora de sincronización y los datos finalmente coherentes

*   Prueba

## <a name="running-your-application-in-read-only-mode"></a>Ejecución de la aplicación en modo de solo lectura

toouse almacenamiento RA-GRS, debe ser capaz de toohandle ambos no se pudo las solicitudes de lectura y actualización de solicitudes con error (con actualización en este caso lo que significa que las inserciones, actualizaciones y eliminaciones). Si leer hello se produce un error del centro de datos principal, las solicitudes pueden ser redirigido toohello centro de datos secundario, pero no de solicitudes de actualización porque Hola secundaria es de solo lectura. Por esta razón, necesita algunos toorun manera su aplicación en modo de solo lectura.

Por ejemplo, puede establecer una marca que se va a comprobar antes de enviar cualquier servicio de almacenamiento de toohello de las solicitudes de actualización. Cuando una de las solicitudes de actualización de hello llega a través de, puede omitirlo y devolver a un cliente de toohello respuesta adecuada. Incluso puede desea toodisable cierto completamente características hasta que se solucione el problema de Hola y notificar a los usuarios que esas características no están disponibles temporalmente.

Si decide toohandle errores para cada servicio por separado, también necesitará toohandle Hola capacidad toorun la aplicación en modo de solo lectura por servicio. Podría tener marcas de solo lectura para cada servicio que se pueden habilitar y deshabilitado y el identificador hello marcador adecuado en lugares adecuados de hello en el código.

Que se va a toorun capaz de la aplicación en modo de solo lectura tiene otra ventaja de lado: ofrece una funcionalidad limitada de hello capacidad tooensure durante una actualización de la aplicación principal. Puede desencadenar la toorun de aplicación en solo lectura modo y punto toohello centro de datos secundario, asegurándose de que nadie tiene acceso a datos de hello en la región principal de hello mientras está realizando las actualizaciones.

## <a name="handling-updates-when-running-in-read-only-mode"></a>Control de las actualizaciones durante la ejecución en modo de solo lectura

Hay muchas maneras de solicitudes de actualización de toohandle cuando se ejecuta en modo de solo lectura. No se va a tratar esto de forma exhaustiva, pero, por lo general, hay un par de patrones que tener en cuenta.

1.  Puede responder tooyour usuario y dígales que actualmente no aceptan actualizaciones. Por ejemplo, un sistema de administración de contactos podría habilitar información de contacto de clientes tooaccess pero no realizar actualizaciones.

2.  Puede poner las actualizaciones en cola en otra región. En este caso, podría escribir la cola de tooa de las solicitudes de actualización pendiente en una región distinta y, a continuación, se tiene un tooprocess de manera esas solicitudes después de centro de datos principal de hello pone de nuevo en línea. En este escenario, se debe comunicar al cliente de Hola que solicitó la actualización Hola se pone en cola para su procesamiento posterior.

3.  Puede escribir las actualizaciones de cuenta de almacenamiento de tooa en otra región. A continuación, al centro de datos principal de hello vuelve a estar conectado, puede tener un toomerge de manera esas actualizaciones de datos principal de hello, dependiendo de la estructura de Hola de datos de Hola. Por ejemplo, si va a crear archivos independientes con una marca de fecha y hora en nombre de hello, puede copiar esos región principal de back-toohello de archivos. Esto funciona para algunas cargas de trabajo como los datos de registro e IoT.

## <a name="handling-retries"></a>Control de los reintentos

¿Cómo saber qué errores se pueden reintentar? Esto viene determinado por la biblioteca de cliente de almacenamiento de Hola. Por ejemplo, un error 404 (recurso no encontrado) no es recuperable porque reintentando no es probable tooresult en correcto. En hello otra parte, un error 500 es recuperable porque es un error del servidor, y puede ser simplemente un problema transitorio. Para obtener más detalles, visite hello [abrir código fuente de hello ExponentialRetry clase](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs) en la biblioteca de cliente de almacenamiento de .NET de Hola. (Busque Hola método ShouldRetry).

### <a name="read-requests"></a>Solicitudes de lectura

Las solicitudes de lectura pueden ser redirigido toosecondary almacenamiento si hay un problema con el almacenamiento principal. Como se indicó anteriormente en [finalmente utilizando los datos coherentes](#using-eventually-consistent-data), debe ser aceptable para su aplicación toopotentially lea datos obsoletos. Si usas tooaccess datos RA-GRS de la biblioteca de cliente del almacenamiento hello, puede especificar el comportamiento de reintento de Hola de una solicitud de lectura estableciendo un valor para hello **LocationMode** tooone de propiedad de siguientes hello:

*   **Principal solo** (Hola predeterminado)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

Al establecer hello **LocationMode** demasiado**PrimaryThenSecondary**, si Hola inicial lectura extremo primario de solicitud toohello se produce un error recuperable, cliente de hello automáticamente realiza otra lectura solicitud de extremo secundario toohello. Si el error de hello es un tiempo de espera del servidor, cliente hello tendrá toowait para tooexpire de tiempo de espera de hello antes de recibir un error irreproducible del servicio de Hola.

Existen básicamente dos escenarios tooconsider cuando decida cómo error irreproducible de toorespond tooa:

*   Se trata de un problema de aislamiento y extremo principal de las solicitudes posteriores toohello no devolverá un error irreproducible. Un ejemplo de cuándo puede ocurrir esto es un error de red transitorio.

    En este escenario, no hay ninguna reducción significativa del rendimiento en tener **LocationMode** establecido demasiado**PrimaryThenSecondary** como solo se produce con poca frecuencia.

*   Se trata de un problema con al menos uno de los servicios de almacenamiento de hello en la región principal de Hola y todos los servicios de toothat las solicitudes posteriores en la región principal de hello son errores puede reintentar de tooreturn probable durante un período de tiempo. Un ejemplo de esto es si la región principal de hello es completamente inaccesible.

    En este escenario, hay una reducción del rendimiento porque todas las solicitudes de lectura se pruebe extremo principal de hello en primer lugar, espere a que tooexpire de tiempo de espera de Hola y cambiar extremo secundario toohello.

Para estos escenarios, debe identificar que hay un problema en curso con el extremo principal de Hola y enviar todas las solicitudes de lectura directamente Hola toohello extremo secundario estableciendo **LocationMode** propiedad demasiado **SecondaryOnly**. En este momento, también debe cambiar hello toorun de aplicación en modo de solo lectura. Este enfoque se denomina hello [patrón de disyuntor](https://msdn.microsoft.com/library/dn589784.aspx).

### <a name="update-requests"></a>Solicitudes de actualización

patrón de disyuntor de Hello también puede ser solicitudes de tooupdate aplicado. Sin embargo, las solicitudes de actualización no pueden ser redirigido toosecondary almacenamiento, que es de solo lectura. Para estas solicitudes, debe dejar hello **LocationMode** propiedad establecida demasiado**principal solo** (Hola de forma predeterminada). toohandle estos errores, puede aplicar un solicita toothese métrica: como 10 errores en una fila y cuando se cumpla el umbral, cambie la aplicación hello en modo de solo lectura. Puede usar Hola los mismos métodos para devolver el modo de tooupdate como los descritos a continuación en la siguiente sección sobre el patrón de disyuntor de Hola de Hola.

## <a name="circuit-breaker-pattern"></a>Patrón de disyuntor

Utilizar el patrón de disyuntor de hello en la aplicación puede impedir que volver a intentar una operación que es probable que toofail repetidamente. Permite Hola aplicación toocontinue toorun en lugar de ocupando tiempo mientras se vuelve a intentar la operación de hello exponencialmente. También detecta cuando se ha corregido el error de hello, en el que aplicación hello en tiempo puede intentar de nuevo la operación de Hola.

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>¿Cómo tooimplement Hola patrón de disyuntor

tooidentify que hay un problema en curso con un punto de conexión principal, puede supervisar la frecuencia con el cliente de hello detecta errores puede intentar de nuevo. Puesto que cada caso es diferente, tendrá que toodecide de umbral de hello desee toouse por extremo secundario de hello decisión tooswitch toohello y ejecutar la aplicación hello en modo de solo lectura. Por ejemplo, podría decidir conmutador de hello tooperform si hay 10 errores en una fila con ningún correctas. Otro ejemplo es tooswitch si se producen errores de 90% de las solicitudes de hello en un periodo de 2 minutos.

Para el primer escenario hello, simplemente puede mantener un recuento de errores de hello y, si se produce un estado correcto antes de llegar a Hola Hola máximo, establezca recuento atrás toozero. Para el segundo escenario hello, una manera de tooimplement es toouse Hola objeto MemoryCache (en. NET). Para cada solicitud, agregar una caché de toohello CacheItem, establecer el valor de hello toosuccess (1) o producirá un error (0) y establecer minutos too2 Hola expiración desde ahora (o lo que la restricción de tiempo). Cuando se alcanza la fecha de expiración de la entrada, se quita automáticamente la entrada de Hola. Esto le dará un intervalo gradual de 2 minutos. Cada vez que realice un servicio de almacenamiento de toohello de solicitud, realice primero una consulta Linq en hello MemoryCache objeto toocalculate Hola porcentaje de operaciones correctas suma los valores de hello y dividiendo por recuento de Hola. Al éxito de porcentaje de hello cae por debajo de algún umbral (por ejemplo, 10%), establezca hello **LocationMode** propiedad para las solicitudes de lectura demasiado**SecondaryOnly** y cambiar la aplicación hello en modo de solo lectura antes de continuar.

umbral de Hola de errores utiliza toodetermine al conmutador de hello toomake puede variar con respecto tooservice de servicio en la aplicación, por lo que debe considerar hacerlos parámetros configurables. Esto también es donde decide toohandle puede reintentar errores de cada servicio por separado o como una de ellas, según lo descrito anteriormente.

Otra consideración es cómo toohandle varias instancias de una aplicación y qué toodo para detectar errores puede reintentar en cada instancia. Por ejemplo, puede tener 20 máquinas virtuales que se ejecutan con hello cargado de la misma aplicación. ¿Va a controlar cada instancia por separado? Si una instancia empieza a tener problemas, ¿desea toolimit Hola respuesta toojust que una instancia, o desea tootry toohave todas las instancias responden en hello mismo vista cuando una instancia tiene un problema? Control de instancias de Hola por separado es mucho más sencillo que intentar respuesta de hello toocoordinate por encima de ellos, pero forma de hacerlo depende de la arquitectura de la aplicación.

### <a name="options-for-monitoring-hello-error-frequency"></a>Opciones para supervisar la frecuencia de error de Hola

Tiene tres opciones principales para supervisar la frecuencia de Hola de reintentos en la región principal de hello en orden toodetermine cuando tooswitch por región secundaria toohello y cambio Hola toorun de aplicación en modo de solo lectura.

*   Agregue un controlador para hello [ **reintentando** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx) evento en hello [ **OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx) objeto pasar las solicitudes de almacenamiento de tooyour: se trata de Hola método se muestra en este artículo y se usa en hello que acompaña a ejemplo. Estos eventos se activan cada vez que el cliente hello intenta enviar una solicitud, lo que le tootrack con qué frecuencia cliente hello encuentra errores puede reintentar en un punto de conexión principal.

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   Hola [ **Evaluate** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx) método en una directiva de reintentos personalizado, puede ejecutar código personalizado siempre que realiza un reintento. En suma toorecording cuando un reintento ocurre, esto también proporciona Hola oportunidad toomodify su comportamiento para reintentar.

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   Hola tercer enfoque es un componente de supervisión personalizado en la aplicación que hace ping continuamente en el punto de conexión de almacenamiento principal con ficticia tooimplement leer las solicitudes (por ejemplo, para leer un blob pequeño) toodetermine su estado. Esto consumiría recursos, pero no en cantidades notables. Cuando se detecta un problema que alcanza el umbral, a continuación, podría ejecutar conmutador Hola demasiado**SecondaryOnly** y modo de solo lectura.

En algún momento, le interesará extremo principal de tooswitch toousing atrás hello y permitir actualizaciones. Si usa uno de los dos primeros métodos de hello mencionados anteriormente, puede simplemente cambiar punto de conexión principal toohello back- y habilitar el modo de actualización después de haber realizado un período de tiempo seleccionado arbitrariamente o un número de operaciones. A continuación, puede dejar que vaya a través de la lógica de reintento de Hola de nuevo. Si se ha corregido el problema de hello, continuará extremo principal de toouse hello y permitir las actualizaciones. Si hay un problema, una vez más se cambiarán extremo secundario toohello atrás y modo de solo lectura después de un error de criterios de Hola que haya establecido.

Para el tercer escenario hello, al hacer ping punto de conexión de almacenamiento principal de hello vuelve correctamente, puede desencadenar nuevo conmutador de hello demasiado**principal solo** y continuar permitir actualizaciones.

## <a name="handling-eventually-consistent-data"></a>Control de datos con coherencia final

RA-GRS funciona mediante la replicación de las transacciones de la región secundaria de hello toohello principal. Este proceso de replicación garantiza que se datos hello en la región secundaria hello *coherente*. Esto significa que todas las transacciones de hello en la región principal de hello finalmente aparecerán en la región secundaria de hello, pero que puede haber un retraso antes de que aparezcan y que no hay ninguna garantía de las transacciones de hello llegan en la región secundaria de Hola Hola mismo orden que en el que se aplicaron originalmente en la región principal de Hola. Si las transacciones llegan en la región secundaria de hello desordenados, se *puede* tenga en cuenta los datos en hello región secundaria toobe en un estado incoherente hasta que el servicio de hello pone al mismo nivel.

Hello tabla siguiente muestra un ejemplo de qué puede ocurrir al actualizar detalles de Hola de un empleado toomake ella un miembro de hello *administradores* rol. Para simplificar hello en este ejemplo, esto requiere actualizar hello **empleado** entidad y actualizar una **rol de administrador** entidad con un recuento del número total de Hola de administradores. Tenga en cuenta cómo se aplican las actualizaciones de hello fuera de servicio en la región secundaria Hola.

| **Hora** | **Transacción**                                            | **Replicación**                       | **Hora de última sincronización** | **Resultado** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | Transacción A: <br> Insertar entidad <br> empleado en región primaria |                                   |                    | La transacción A inserta tooprimary,<br> aún sin replicar. |
| T1       |                                                            | Transacción A <br> replicada en<br> región secundaria | T1 | La transacción A replica toosecondary. <br>Hora de última sincronización actualizada.    |
| T2       | Transacción B:<br>Actualizar<br> entidad empleado<br> en región primaria  |                                | T1                 | Transacción B escrito tooprimary,<br> aún sin replicar.  |
| T3       | Transacción C:<br> Actualizar <br>administrator<br>entidad rol administrador en región<br>primary |                    | T1                 | Transacción C escrito tooprimary,<br> aún sin replicar.  |
| *T4*     |                                                       | Transacción C <br>replicada en<br> región secundaria | T1         | Transacción C replica toosecondary.<br>LastSyncTime no actualizado porque <br>la transacción B está aún sin replicar.|
| *T5*     | Leer entidades <br>desde región secundaria                           |                                  | T1                 | Obtener valor obsoleto de Hola de empleado <br> empleado porque la transacción B aún <br> no se ha replicado. Obtener el nuevo valor de Hola para<br> entidad rol de administrador porque C<br> se ha replicado. La hora de la última sincronización aún no se ha<br> actualizado porque la transacción B<br> no se ha replicado. Puede ver que la<br>entidad rol de administrador es incoherente <br>porque Hola entidad fecha y hora es posterior a <br>Hola hora de última sincronización. |
| *T6*     |                                                      | Transacción B<br> replicada en<br> región secundaria | T6                 | *T6*: todas las transacciones hasta la C <br>se han replicado, Hora de última sincronización<br> se ha actualizado. |

En este ejemplo, suponga Hola cliente conmutadores tooreading de región secundaria de Hola a T5. Puede leer correctamente hello **rol de administrador** entidad en este momento, pero la entidad de hello contiene un valor para el número de Hola de los administradores que no es coherente con el número de Hola de **empleado** entidades que se marcan como administradores en la región secundaria de hello en este momento. El cliente podría mostrar simplemente este valor, con el riesgo de Hola que es información incoherente. O bien, el cliente de hello podría intentar toodetermine ese hello **rol de administrador** está en un estado potencialmente incoherente porque Hola actualizaciones han tenido lugar fuera de servicio y, a continuación, informar al usuario de Hola de este hecho.

toorecognize que tiene datos potencialmente incoherentes, cliente hello puede utilizar el valor de Hola de hello *hora de última sincronización* que puede obtener en cualquier momento al consultar un servicio de almacenamiento. Esto indica tiempo hello cuando datos hello en la región secundaria Hola por últimos coherente y al servicio Hola aplicado todos Hola transacciones toothat anterior punto en el tiempo. En el ejemplo de Hola mostrado anteriormente, una vez que el servicio de hello inserta hello **empleado** entidad región secundaria de hello, Hola hora de última sincronización se establece demasiado*T1*. Permanece en *T1* hasta que actualiza el servicio de Hola Hola **empleado** entidad en la región secundaria de Hola y se establece demasiado*T6*. Si el cliente de hello recupera Hola última hora de sincronización cuando lee la entidad de hello en *T5*, puede comparar con marca de tiempo de hello en la entidad de Hola. Si es posterior a Hola Hola marca de tiempo en la entidad de Hola tiempo, de la última sincronización, a continuación, hello entidad se encuentra en un estado incoherente potencialmente y puede requerir sea cual sea la acción adecuada de hello para la aplicación. Uso de este campo requiere que sepa cuándo se completó toohello de actualización de última de hello principal.

## <a name="testing"></a>Prueba

Es importante tootest que la aplicación se comporta según lo esperado cuando encuentra errores puede intentar de nuevo. Por ejemplo, debe tootest que Hola toohello de conmutadores de aplicación secundario y en modo de solo lectura cuando se detecta un problema y vuelve cuando región principal Hola vuelva a estar disponible. toodo, necesita una manera toosimulate puede reintentar los errores y controlar con qué frecuencia se producen.

Puede usar [Fiddler](http://www.telerik.com/fiddler) toointercept y modificar las respuestas HTTP en una secuencia de comandos. Esta secuencia de comandos puede identificar las respuestas que proceden de su punto de conexión principal y cambiar tooone de código de estado HTTP de Hola que Hola que biblioteca cliente de almacenamiento se reconoce como un error irreproducible. Este fragmento de código muestra un ejemplo sencillo de una secuencia de comandos de Fiddler que intercepta las solicitudes de tooread de respuestas contra Hola **employeedata** tabla tooreturn un estado 502:

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

También puede extender este ejemplo toointercept una gama más amplia de solicitudes y cambiar sólo hello **responseCode** en algunos de ellos toobetter simular un escenario real. Para obtener más información acerca de cómo personalizar las secuencias de comandos de Fiddler, consulte [modificar una solicitud o respuesta](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse) Hola documentación de Fiddler.

Si ha realizado los umbrales de Hola para cambiar el modo de solo tooread de aplicación configurable, resultará más fácil de comportamiento de hello tootest con volúmenes de transacciones no es de producción.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información acerca de acceso de lectura la redundancia geográfica, incluidos otro ejemplo de cómo está configurado Hola LastSyncTime, visite [opciones de redundancia de almacenamiento de Windows Azure y almacenamiento con redundancia geográfica acceso de lectura](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

* Para obtener un ejemplo completo que muestra cómo toomake Hola conmutador y hacia atrás entre los extremos de principal y secundaria de hello, vea [ejemplos de Azure: mediante Hola patrón de disyuntor con almacenamiento de RA-GRS](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs).
