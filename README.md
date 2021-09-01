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

#

## Terminologia
**Ticket Granting Ticket (TGT):** un ticket de concesión de tickets es un ticket de autenticación que se utiliza para solicitar tickets de servicio del TGS para recursos específicos del dominio.

**Centro de distribución de claves (KDC) :** el Centro de distribución de claves es un servicio para emitir TGT y tickets de servicio que constan del Servicio de autenticación y el Servicio de concesión de tickets.

**Servicio de autenticación (AS) :** el servicio de autenticación emite TGT para que los utilice el TGS en el dominio  para solicitar acceso a otras máquinas y tickets de servicio.

**Servicio de concesión de tickets (TGS) :** el servicio de concesión de tickets toma el TGT y devuelve un ticket a una máquina del dominio.

**Nombre principal de servicio (SPN) :** un nombre principal de servicio es un identificador que se le da a una instancia de servicio para asociar una instancia de servicio con una cuenta de servicio de dominio. Windows requiere que los servicios tengan una cuenta de servicio de dominio, por lo que un servicio necesita un conjunto de SPN.

**Clave secreta a largo plazo de KDC (clave KDC LT)  :** la clave KDC se basa en la cuenta de servicio KRBTGT. Se utiliza para cifrar el TGT y firmar el PAC.

**Clave secreta a largo plazo del cliente (clave LT del cliente)  :** la clave del cliente se basa en la computadora o la cuenta de servicio. Se utiliza para verificar la marca de tiempo cifrada y cifrar la clave de sesión.

**Clave secreta de servicio a largo plazo (clave de servicio LT)  :** la clave de servicio se basa en la cuenta de servicio. Se utiliza para cifrar la parte del servicio del ticket de servicio y firmar el PAC.

**Clave de sesión :** emitida por el KDC cuando se emite un TGT. El usuario proporcionará la clave de sesión al KDC junto con el TGT cuando solicite un ticket de servicio.

**Certificado de atributo de privilegio (PAC) :** el PAC contiene toda la información relevante del usuario, se envía junto con el TGT al KDC para ser firmado por la clave Target LT y la clave KDC LT para validar al usuario.

**KRBTGT:** Es un ticket especial que no esta asignado a un usuario en concreto. 

#

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

El KDC le entregará a Alberto un TGS, dandole acceso a los servicios que le haya solicitado. Este nuevo ticket tiene fecha de caducidad, por lo que pasado el tiempo, deberemos de pedir un nuevo ticket. 


#
### Instalando y configurando Kerberos
### Atacando Kerberos
#### Kerbrute
Kerbrute es una popular herramienta de enumeración que se utiliza para forzar y enumerar usuarios válidos del directorio activo mediante el abuso de la autenticación previa de Kerberos. Puede descarga kerbrute desde aqui: https://github.com/ropnop/kerbrute/releases  (Tiene varias versiones, eliga según su arquitectura)
Cuando se usa la fuerza bruta a través de Kerberos, se puede usar la fuerza bruta enviando solo un único marco UDP al KDC, lo que le permite enumerar los usuarios del dominio a partir de una lista de palabras. Esto evitará que el administrador de sistema pueda detectar un inusual numero de peticiones de autenticación frente a kerberos

*Metodo de utilización*
```
./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt
```

`./kerbrute` Ejecutamos kerbrute, **recordar dar permisos de ejecución.**

`userenum` Le decimos a kerbrute que queremos enumerar usuarios dentro de kerberos

`--dc` Marca la ubicación del controlador de dominio (KDC) al que apuntar. Si está en blanco, se buscará a través de DNS

`CONTROLLER.local` Es un servidor DNS de prueba

`-d` El dominio completo a usar

`User.txt` Lista de texto que contiene nombre de usuarios comunes para probar si dichos usuarios se enecuentran en la enumeración


#
#### Kerberoasting - Rubeus
Kerberoasting permite a un usuario solicitar un ticket de servicio para cualquier servicio con un SPN registrado y luego usar ese ticket para descifrar la contraseña del servicio. Si el servicio tiene un SPN registrado, entonces puede ser Kerberoastable; sin embargo, el éxito del ataque depende de cuán fuerte sea la contraseña y si es rastreable, así como de los privilegios de la cuenta de servicio crackeada.

Para realizar esta acción utilizaremos **Rubeus**
![kerberoasting](https://user-images.githubusercontent.com/87484792/131710134-fc707d2f-6f92-437b-b0df-fb736c7b6bec.png)

Como podemos observar en la imagen, hemos conseguido un HASH. Este hash lo guardaremos en nuestra maquina atacante, lo meteremos en un archivo e intentaremos a traves de herramientas ( en este caso hashcat ) obtener en texto claro la contraseña. 

Ejemplo de uso:
``` hashcat -m 13100 -a 0 hash.txt Pass.txt```

**En este post no se explicará el uso de hashcat**
# 
### AS-REP - Rubeus 
AS-REP Roasting vuelca los hashes krbasrep5 de las cuentas de usuario que tienen la autenticación previa de Kerberos deshabilitada. A diferencia de Kerberoasting, estos usuarios no tienen que ser cuentas de servicio, el único requisito para poder tostar AS-REP a un usuario es que el usuario debe tener la autenticación previa desactivada.

**Descripción general de tostado AS-REP**

Durante la autenticación previa, el hash de los usuarios se utilizará para cifrar una marca de tiempo que el controlador de dominio intentará descifrar para validar que se está utilizando el hash correcto y que no se está reproduciendo una solicitud anterior. Después de validar la marca de tiempo, el KDC emitirá un TGT para el usuario. Si la autenticación previa está deshabilitada, puede solicitar cualquier dato de autenticación para cualquier usuario y el KDC devolverá un TGT cifrado que se puede descifrar sin conexión porque el KDC omite el paso de validar que el usuario es realmente quien dice ser.

![l3wJhby](https://user-images.githubusercontent.com/87484792/131713005-77038b03-6e82-4572-866b-c4ed142186ac.png)

-Como se puede comprobar, el paso es muy similar con Rubeus-


#### Pass the Ticket - mimikatz
#### Golden/Silver Ticket Attack
