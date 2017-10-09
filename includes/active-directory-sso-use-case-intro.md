Las organizaciones están usando más aplicaciones de [Software como servicio (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) para aumentar la productividad dado que la tecnología y las herramientas de nube son cada vez más fáciles de obtener. A medida que aumenta el número de Hola de aplicaciones de SaaS, se convierte en un desafío para las cuentas de toomanage de los administradores de Hola y derechos de acceso y para Hola tooremember a los usuarios sus contraseñas diferentes. La administración de esas aplicaciones individualmente crea más trabajo y es menos seguro.

* Los empleados que tienen un seguimiento de tookeep de las contraseñas suelen toouse menos seguras tooremember métodos ellos, ya sea escribirlas o mediante Hola mismas contraseñas a través de varias cuentas.
* Cuando llega un nuevo empleado o se marcha uno, todas sus cuentas deben ser aprovisionadas o desaprovisionadas individualmente.
* Además, los empleados pueden comenzar a usar aplicaciones SaaS para su trabajo sin tener que pasar a través de departamentos de TI, lo que significa que va a crear sus propias cuentas en sistemas que Hola a los administradores de TI no han aprobado y no son de supervisión.  

Es una solución para todos estos desafíos es el inicio de sesión único (SSO). Ha Hola toomanage de manera más sencilla de varias aplicaciones y proporcionar a los usuarios una experiencia coherente de inicio de sesión. Azure Active Directory (Azure AD) proporciona una solución sólida de SSO y tiene muchas aplicaciones previamente integradas disponibles, con los tutoriales para que los administradores tooquickly, configurar una nueva aplicación e iniciar el aprovisionamiento de usuarios.

## <a name="how-does-azure-active-directory-integrate-apps"></a>¿Cómo integra Azure Active Directory las aplicaciones?
Azure AD permite toointegrate sus aplicaciones y el aprovisionamiento de cuentas. Esto puede hacerse a través de uno de estos dos enfoques.

* Si la aplicación hello previamente se integra en la aplicación hello galería, puede ir a través de ese portal tooset seguridad de aplicaciones y configurar Hola configuración tooallow SSO. Para cualquier aplicación de la galería, puede empezar a seguimiento Hola simple paso a paso las instrucciones presentadas en Galería de aplicaciones de Hola y Hola tooenable portal Azure inicio de sesión único.
* Si la aplicación hello no está en la Galería de hello, puede configurar mayoría de las aplicaciones de Azure AD como una aplicación personalizada. Esto requiere un poco más técnica tooconfigure de conocimientos. Puede agregar cualquier aplicación que admita SAML 2.0 como aplicación federada o cualquier aplicación que tenga una página de inicio de sesión basada en HTML para usar SSO con contraseña.

Hola caso donde los usuarios han creado sus propias cuentas para las aplicaciones SaaS que no están administradas por TI, hello [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md) herramienta proporciona una solución. Esta herramienta supervisa hello web tráfico tooidentify qué aplicaciones se usan en toda la organización de Hola y número de Hola de personas que utilizan cada uno de ellos. TI puede usar esta información toolearn qué usuarios de hello aplicaciones prefieran y Decisión qué toointegrate en Azure AD para SSO.  

Al integrar una aplicación en Azure AD, puede asignar las identidades de los usuarios de hello aplicación establecida identidades tootheir AD de Azure respectiva.  

