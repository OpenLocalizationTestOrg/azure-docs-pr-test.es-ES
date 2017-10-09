Una zona DNS es toohost usado Hola registros DNS para un dominio en particular. toostart hospedaje de su dominio de DNS de Azure, necesita toocreate una zona DNS para ese nombre de dominio. Cada registro DNS del dominio se crea luego en esta zona DNS.

Por ejemplo, dominio hello 'contoso.com' puede contener varios registros DNS, como 'mail.contoso.com' (para un servidor de correo electrónico) y 'www.contoso.com' (para un sitio web).

Al crear una zona DNS de Azure DNS:

* Hola nombre de zona de hello debe ser único dentro del grupo de recursos de Hola y zona hello no debe existir ya. En caso contrario, se produce un error en operación de Hola.
* Hola se puede reutilizar el mismo nombre de zona en otro grupo de recursos o una suscripción de Azure diferente.
* Que comparten varias zonas hello mismo nombre, cada instancia se asigna direcciones de servidor de otro nombre. Solo un conjunto de direcciones puede configurarse con el registrador de nombres de dominio de Hola.

> [!NOTE]
> No es necesario tooown un toocreate de nombre de dominio una zona DNS con ese nombre de dominio en DNS de Azure. Sin embargo, es necesario servidores de nombres DNS de Azure de tooown Hola dominio tooconfigure Hola Hola servidores de nombres correcta para nombre de dominio de hello con el registrador de nombres de dominio de Hola.
> 
> Para obtener más información, consulte [delegar un tooAzure de dominio DNS](../articles/dns/dns-domain-delegation.md).
