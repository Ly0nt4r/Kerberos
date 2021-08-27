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
Éste es quién mantiene las bases de datos (o el servicio, equipo, usuarios, servidor...) con la información de las cuentas de seguridad.
El KDC almacena una clave criptográfica que sólo conocen la entidad de seguridad y el KDC. Esta clave se utiliza en los intercambios entre la entidad de seguridad y el KDC.
Cuando el cliente quiere hablar (acceder) a un recursos (ubicado en un servidor), el cliente envía una solicitud al KDC y éste distribuye una clave de sesión única para que ambas partes se autentiquen mutuamente.

**EJEMPLO PRACTICO**
```
Alberto ha entrado a trabajar a una empresa como contable, en ella, tienen una planta dedicada unicamente a su puesto de trabajo.
La plantilla es amplia, y todos los trabajadores necesitan acceder a una base de datos central donde controlar temas contables (albaranes,facturas,salarios)

Para ello el técnico informatico ha levantado un directorio activo en la planta, donde ha implementado el protocolo Kerberos.

Ahora todos los trabajadores podrán acceder de forma centralizada a aquella base de dato, pero para ello necesitarán decirle a Kerberos que se tratan de un trabajador más,
y no de un infiltrado, ya que la información que contiene dicha base de datos es contenido altamente sensible.

¿COMO SE REALIZA EL PROCESO?
Mira a continuación...
```

## HOLA SOY ALBERTO
![pixlr-bg-result](https://user-images.githubusercontent.com/87484792/131126333-81d13c99-d3b8-4f53-841c-791ea89da567.png)

Hoy es mi primer día en la empresa y deseo acceder a la base de datos para consultar las nominas de este mes.
#

![pixlr-bg-result (1)](https://user-images.githubusercontent.com/87484792/131130255-fcfb5f58-9279-4e08-b939-f3ab2971fedb.png)

Alberto se logueará en el KDC desde su ordenador, en la red de AD.
#

![pixlr-bg-result (2)](https://user-images.githubusercontent.com/87484792/131131210-e7525441-ddcc-4568-a512-72d957982d25.png)

El KDC le enviará a Alberto el TGT encriptado con su contraseña (Clave Secreta). 
#

![pixlr-bg-result (1)](https://user-images.githubusercontent.com/87484792/131130255-fcfb5f58-9279-4e08-b939-f3ab2971fedb.png)![QFeXDN0 (1)](https://user-images.githubusercontent.com/87484792/131131621-39b66f29-93ab-4172-aca5-34018694ebfd.png)

Alberto desencriptará el TGT puesto que conoce y posee su clave secreta, y se las volverá a enviar al KDC.
#

![pixlr-bg-result (3)](https://user-images.githubusercontent.com/87484792/131132499-3cad1b7d-d93b-477c-83b0-1520969bc096.png)![pixlr-bg-result (4)](https://user-images.githubusercontent.com/87484792/131132849-9669bda1-3b9e-4d62-b320-572e870db5e7.png)

El KDC le entregará a Alberto un TGS, dandome acceso a los servicios que le haya solicitado. Este nuevo ticket tiene fecha de caducidad, por lo que pasado el tiempo, deberemos de pedir un nuevo ticket. 


#
### Instalando y configurando Kerberos
### Atacando Kerberos
#### Kerbrute
#### Kerberoasting - Rubeus
#### Pass the Ticket - mimikatz
#### Golden/Silver Ticket Attack
