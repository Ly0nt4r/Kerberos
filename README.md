# KERBEROS
![kerbweblogo (1)](https://user-images.githubusercontent.com/87484792/131123599-fed87e5c-3701-4648-8483-d48433b54810.png)
#
## Todo sobre Kerberos
#
### Funcionamiento (verificación, tickets, validación...)

El protocolo de autenticación Kerberos lo que proporciona es un mecanismo que permite la autenticación entre cliente y servidor.
Éste se basa en una técnica de autenticación basada en secretos compartidos. Es decir, si 2 personas conocen el secreto cualquiera de ellas puede verifica la identidad de la otra (teniendo en cuenta que conoce el secreto).
Cuando un equipo se valida al dominio presenta una autenticación (información encriptada en la clave secreta).
El equipo que va a conceder el acceso, recibe esa petición y lo descifra. Si sabe leer el contenido el descifrado se ha realizado correctamente y puede ver que el equipo que ha presentado la petición tiene la clave correcta, o una autorización a entrar, donde previamente se te ha asignado permisos.
El ticket tiene un periodo de vida. Trascurrido ese periodo el ticket necesita ser renovado.
**El KDC (Key Distribution Center)**
Éste es quién mantiene la base de datos (o el servicio, equipo, servidor...) con la información de las cuentas de seguridad.
El KDC almacena una clave criptográfica que sólo conocen la entidad de seguridad y el KDC. Esta clave se utiliza en los intercambios entre la entidad de seguridad y el KDC.
Cuando el cliente quiere hablar (acceder) a un recursos (ubicado en un servidor), el cliente envía una solicitud al KDC y éste distribuye una clave de sesión única para que ambas partes se autentiquen mutuamente.

#
### Instalando y configurando Kerberos
### Atacando Kerberos
#### Kerbrute
#### Kerberoasting - Rubeus
#### Pass the Ticket - mimikatz
#### Golden/Silver Ticket Attack
