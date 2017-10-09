Hola sistema de nombres de dominio (DNS) es recursos toolocate usado en hello internet. Por ejemplo, cuando escriba una dirección de la aplicación web en el explorador, o haga clic en un vínculo en una página web, utiliza dominio DNS tootranslate hello en una dirección IP. dirección IP de Hello es algo parecido a una dirección postal, pero no resulta sencillo muy humano. Por ejemplo, es un nombre DNS como mucho más fácil tooremember **contoso.com** es tooremember una dirección IP como 192.168.1.88 o 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Hola sistema DNS se basa en *registros*. Los registros asocian un *nombre*específico, como **contoso.com**, a una dirección IP u otro nombre DNS. Cuando una aplicación, como un explorador web, busca un nombre en DNS, se encuentra el registro de hello y utiliza lo señala tooas Hola dirección. Si Hola valor toois de puntos de una dirección IP, el Explorador de hello utilizará ese valor. Si señala tooanother nombre DNS, aplicación hello tiene resolución toodo nuevo. En última instancia, todas las resoluciones de nombre terminarán en una dirección IP.

Cuando se crea una aplicación web en el servicio de aplicaciones, automáticamente se asigna un nombre DNS toohello web app. Este nombre toma la forma de Hola de  **&lt;yourwebappname&gt;. azurewebsites.net**. También hay una dirección IP virtual disponible para su uso cuando se registra la creación de DNS, por lo que puede crear registros de ese punto toohello **. azurewebsites.net**, o puede apuntar toohello dirección IP.

> [!NOTE]
> dirección IP de saludo de la aplicación web cambiará si elimina y volver a crear la aplicación web o cambiar Hola modo del plan de servicio de aplicaciones también**libre** después de que se ha establecido demasiado**básica**, **Shared**, o **estándar**.
> 
> 

También hay varios tipos de registros, cada uno con sus propias funciones y limitaciones, pero para las aplicaciones web, solo nos interesan dos, los registros *D* y *CNAME*.

### <a name="address-record-a-record"></a>Registro de dirección (registro D)
Un registro a un dominio, asigna como **contoso.com** o **www.contoso.com**, *o un dominio comodín* como  **\*. contoso.com**, dirección IP de tooan. En caso de hello de una aplicación web en el servicio de aplicaciones, ya sea Hola dirección IP virtual del servicio de Hola o una dirección IP específica que adquirió para la aplicación web.

Hola ventajas principales de un registro a través de un registro CNAME son:

* Puede asignar un dominio raíz como **contoso.com** dirección IP de tooan; registradores muchos sólo admiten este uso de registros
* Puede disponer de una entrada que utilice un carácter comodín, como **\*.contoso.com**, que administraría las solicitudes de varios subdominios como **mail.contoso.com**, **blogs.contoso.com** o **www.contso.com**.

> [!NOTE]
> Puesto que está asignado a un registro tooa una dirección IP estática, no puede resolver automáticamente la dirección IP de toohello de cambios de la aplicación web. Se proporciona una dirección IP para su uso con registros al configurar las opciones de nombre de dominio personalizado para su aplicación web; Sin embargo, puede cambiar este valor si eliminar y volver a crear la aplicación web o cambiar hello tooback de modo de plan de servicio de aplicaciones también**libre**.
> 
> 

### <a name="alias-record-cname-record"></a>Registro de alias (registro CNAME)
Un registro CNAME asigna un *específico* de nombres DNS, como **mail.contoso.com** o **www.contoso.com**, nombre de dominio (canónico) tooanother. En caso de hello de aplicaciones Web de servicio de aplicación, nombre de dominio canónico hello es hello  **&lt;yourwebappname >. azurewebsites.net** nombre de dominio de la aplicación web. Una vez creado, Hola CNAME crea un alias para hello  **&lt;yourwebappname >. azurewebsites.net** nombre de dominio. Hola entrada CNAME resolverá toohello dirección IP de su  **&lt;yourwebappname >. azurewebsites.net** nombre de dominio automáticamente, por lo que si se cambia la dirección IP de Hola de aplicación web de hello, no tiene tootake ninguna acción.

> [!NOTE]
> Algunos registradores de dominios sólo permiten subdominios toomap cuando se usan como un registro CNAME, **www.contoso.com**y no raíz nombres, como **contoso.com**. Para obtener más información sobre los registros CNAME, vea documentación de hello proporcionada por el registrador, <a href="http://en.wikipedia.org/wiki/CNAME_record">Hola entrada de Wikipedia en el registro CNAME</a>, o hello <a href="http://tools.ietf.org/html/rfc1035">nombres de dominio de IETF: implementación y especificación</a> documento.
> 
> 

### <a name="web-app-dns-specifics"></a>Detalles de DNS de aplicación web
Uso de un registro con las aplicaciones Web requiere toofirst crear uno de los siguientes registros TXT de hello:

* **Para el dominio raíz de hello** -registro TXT de DNS A de  **@**  demasiado  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Para un subdominio específico** -nombre de DNS A  **&lt;subdominio >** demasiado**&lt;yourwebappname&gt;. azurewebsites.net**. Por ejemplo, **blogs** si es un registro de hello para **blogs.contoso.com**.
* **Para hello comodín sub-dodmains** -registro TXT de DNS A de *** demasiado  **&lt;yourwebappname&gt;. azurewebsites.net**.

Este registro TXT es tooverify usado que posee dominio Hola estás intentando toouse. Se trata además de registro de toocreating un apuntando toohello de dirección IP virtual de la aplicación web.

Puede encontrar la dirección IP de Hola y **. azurewebsites.net** nombres de la aplicación web mediante la realización de Hola lo siguiente:

1. En el explorador, abra hello [Portal de Azure](https://portal.azure.com).
2. Hola **aplicaciones Web** hoja, haga clic en nombre de saludo de la aplicación web y, a continuación, seleccione **los dominios personalizados** desde el final Hola Hola.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Hola **los dominios personalizados** hoja, verá Hola dirección IP virtual. Guarde esta información, puesto que se utilizará al crear registros DNS.
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > No se puede utilizar nombres de dominio personalizado con un **libre** aplicación web y debe actualizar el plan de servicio de aplicación Hola demasiado**Shared**, **básica**, **estándar**, o **Premium** capa. Para obtener más información en hello servicio de aplicaciones plan de los niveles de precios, incluido cómo toochange Hola a nivel de precios de la aplicación web, consulte [cómo tooscale web aplicaciones](../articles/app-service-web/web-sites-scale.md).
   > 
   > 

