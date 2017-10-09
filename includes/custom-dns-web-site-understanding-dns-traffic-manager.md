Hola sistema de nombres de dominio (DNS) es cosas toolocate usado en hello internet. Por ejemplo, cuando se escribe una dirección en un explorador, o haga clic en un vínculo en una página web, utiliza dominio DNS tootranslate hello en una dirección IP. dirección IP de Hello es algo parecido a una dirección postal, pero no resulta sencillo muy humano. Por ejemplo, es un nombre DNS como mucho más fácil tooremember **contoso.com** es tooremember una dirección IP como 192.168.1.88 o 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Hola sistema DNS se basa en *registros*. Los registros asocian un *nombre*específico, como **contoso.com**, a una dirección IP u otro nombre DNS. Cuando una aplicación, como un explorador web, busca un nombre en DNS, se encuentra el registro de hello y utiliza lo señala tooas Hola dirección. Si Hola valor toois de puntos de una dirección IP, el Explorador de hello utilizará ese valor. Si señala tooanother nombre DNS, aplicación hello tiene resolución toodo nuevo. En última instancia, todas las resoluciones de nombre terminarán en una dirección IP.

Cuando se crea un sitio Web de Azure, se asigna automáticamente un nombre DNS toohello sitio. Este nombre toma la forma de Hola de  **&lt;yoursitename&gt;. azurewebsites.net**. Cuando se agrega el sitio Web como un extremo de Azure Traffic Manager, su sitio Web, a continuación, es accesible a través de hello  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** dominio.

> [!NOTE]
> Cuando el sitio Web está configurado como un punto de conexión de administrador de tráfico, usará hello **. trafficmanager.net** dirección cuando la creación de registros DNS.
> 
> Los registros CNAME solo se pueden usar con el Administrador de tráfico
> 
> 

También hay varios tipos de registros, cada uno con sus propias funciones y limitaciones, pero para sitios Web configurados tooas extremos de Traffic Manager, solo ocupa aproximadamente uno; *CNAME* registros.

### <a name="cname-or-alias-record"></a>Registro de CNAME o Alias
Un registro CNAME asigna un *específico* de nombres DNS, como **mail.contoso.com** o **www.contoso.com**, nombre de dominio (canónico) tooanother. En caso de hello de sitios Web de Azure con el Administrador de tráfico, nombre de dominio canónico hello es hello  **&lt;myapp >. trafficmanager.net** nombre de dominio de su perfil de Traffic Manager. Una vez creado, Hola CNAME crea un alias para hello  **&lt;myapp >. trafficmanager.net** nombre de dominio. Hola entrada CNAME resolverá toohello dirección IP de su  **&lt;myapp >. trafficmanager.net** nombre de dominio automáticamente, por lo que si se cambia la dirección IP de hello del sitio Web de hello, no tiene tootake ninguna acción.

Una vez que el tráfico llega en el Administrador de tráfico, a continuación, enruta el sitio Web de tooyour de tráfico hello, mediante está configurado para el método de equilibrio de carga de Hola. Se trata de un sitio Web de tooyour toovisitors completamente transparente. Sólo verán el nombre de dominio personalizado de hello en su explorador.

> [!NOTE]
> Algunos registradores de dominios sólo permiten subdominios toomap cuando se usan como un registro CNAME, **www.contoso.com**y no raíz nombres, como **contoso.com**. Para obtener más información sobre los registros CNAME, vea documentación de hello proporcionada por el registrador, <a href="http://en.wikipedia.org/wiki/CNAME_record">Hola entrada de Wikipedia en el registro CNAME</a>, o hello <a href="http://tools.ietf.org/html/rfc1035">nombres de dominio de IETF: implementación y especificación</a> documento.
> 
> 

