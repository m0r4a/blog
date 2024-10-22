---
title: "Resumen del examen 2 de Criptografía"
draft: false
date: 2024-10-22
description: Es una re-escritura del documento de resumen de la clase de Criptografía.
summary: Este post es una re-escritura del documento de resumen dado por el profesor que incluye solo los temas del examen 2.
---

## Administración de claves

Es administrar las llaves durante todo su tiempo de vida, desde que son creadas hasta que son destruidas, esto incluye el uso, almacenamiento, la asignación, la creación, y destrucción de estas.

Esto nos permite mantener un ecosistema seguro, de manera que cada usuario puede tener acceso a diferentes permisos con una sola llave, como el funcionamiento de las antiguas llaves maestras.

Las llaves pueden ser simétricas (una sola llave) para información que va a estar “en reposo” (es decir que no va a viajar a través de algún medio) como las propias llaves, o asimétricas (dos llaves) para información que va a estar “viajando” entre distintos medios.

Normalmente se utiliza una mezcla de los dos sistemas criptográficos, usando un sistema asimétrico para enviar una llave simétrica, ya que la criptografía simétrica es más rápida, pero no puede transmitir por sí misma la llave de forma segura, por lo que se usa un sistema asimétrico para compartir la llave.

Las llaves simétricas se encuentran cifradas de manera simétrica en un servidor KM (key manager), de manera que el usuario tiene que mandar su certificado (criptografía asimétrica) al servidor KM para compararlo con la autoridad certificadora, y le diga si es en realidad quien dice ser.

Una vez hecho esto, el servidor envía su certificado al cliente para establecer una conexión, y luego el servidor KM descifra la llave simétrica (con otra llave simétrica) y se la manda al usuario a través de un canal TLS.

Las llaves asimétricas conllevan un camino similar, solo que en vez de usar un canal TLS, utiliza la llave pública de los cifrados de cada uno (usuario y servidor) para compartir de manera segura una llave simétrica por medio de un canal (que pudiera no ser seguro), y a su vez la información encriptada con la llave simétrica.

### Proceso de Autenticación y Cifrado Simétrico con Certificados

{{< figure
    src="resources/cifrado_simetrico.svg"
    alt="Imagen de como se ve el cifrado simétrico en un servidor"
    nozoom=true
    class="mx-auto"
>}}

### Proceso de Validación y Cifrado Asimétrico en un Servidor KM

{{< figure
    src="resources/cifrado_asimetrico.svg"
    alt="Imagen de como se ve el cifrado asimétrico en un servidor"
    nozoom=true
    class="mx-auto"
>}}


## Módulo de plataforma segura y usos de TPM

Es básicamente un cripto-procesador, un chip físico que puede venir como un aditamento, como es el caso de la fotografía, o puede estar incrustado en la placa base. Este chip se encarga de almacenar llaves y procesar sistemas criptográficos complejos, de manera que asiste al procesador (CPU), al mismo tiempo que es más seguro ya que únicamente puede conectarse con el procesador, evitando que algún hardware desconocido pueda copiar las llaves o modificar su funcionamiento.

Entre las cosas que se pueden hacer, el TPM puede validar tu identidad utilizando llaves específicas del cripto-procesador (que no pueden ser modificadas) o incluso llaves de otras aplicaciones que son almacenadas dentro del mismo.

También puede validar el sistema operativo, analizando componentes firmados, y si las firmas no coinciden, es porque probablemente el archivo ha sido modificado, lo que podría indicar algún tipo de infección (normalmente esto mismo evita el “secure boot”).

### Distintos usos para el chip TPM
1. DRM (Digital Rights Management)
2. Cifrado de archivos y carpetas
3. Correo electrónico seguro
4. SSL
5. VPN
6. Contraseñas de uso único
7. Administración de cuentas
8. Two-Factor Authentication con las llaves del chip

### Componentes del chip
1. Generador de números aleatorios
2. Generación de claves criptográficas
3. Almacenamiento seguro de llaves
4. Hashes

## Seguridad en Internet

Encontramos la criptografía en muchos lugares distintos, sobre todo en donde se ocupe algún tipo de autenticación, sobre todo cuando se usan contraseñas o certificados.

Existen 3 métodos de autenticación:

{{< figure
    src="resources/metodos_de_auth.svg"
    alt="Tipos de métodos de autentificación"
    nozoom=true
    class="mx-auto"
>}}

La criptografía simétrica es para la información que no se encuentra en tráfico, por su velocidad y facilidad de manejo de llave.

La criptografía asimétrica es para la información que está en tránsito, normalmente se utiliza para el manejo de sesiones, y una vez establecida la conexión se usa criptografía simétrica para el envío de grandes volúmenes de información.

### El problema de la seguridad en el manejo de contraseñas

#### Almacenamiento

Las contraseñas no deben ser guardadas en texto plano, por lo que surge la idea de almacenarlas como el hash de esta, de manera que, si un atacante las roba, no pueda revertirlas.

#### Funciones Hash

{{< alert icon="comment" >}}
Funciones de hash criptográficas ≠ Funciones de hash de contraseñas
{{< /alert >}}

El principal problema es que las funciones de hash criptográficas no están diseñadas para las contraseñas. Tienden a ser muy rápidas, y en general esto sería bueno, si no fuera porque esto beneficia a un atacante que quiera hacer un ataque de fuerza bruta.

#### Reconocimiento

El primer paso a tomar es buscar si la contraseña ya se encuentra en alguna rainbow table en internet, o similar; en caso contrario, se procede a hacer el ataque de fuerza bruta.

#### Velocidad

La velocidad juega un papel crucial, por lo que si el método de hashing es muy rápido (por decir 0.1 segundos), la contraseña puede ser rota en relativamente poco tiempo, por lo que buscamos mantener el proceso de hashing por encima de 0.1 segundos, preferentemente cerca de 1 segundo de velocidad.

#### Sal

La sal es un conjunto de letras generadas aleatoriamente para cada usuario que cambian el hash de salida, lo que dificulta al atacante (computacionalmente imposible) encontrar la contraseña del usuario generada en una rainbow table en internet.

#### Pimienta

Igual que la sal, la pimienta también cambia el hash final, pero suele estar dentro del código fuente. Esto es útil si por algún motivo la base de datos donde estamos guardando las contraseñas no es segura, o no podemos confiar en el tráfico desde la aplicación hasta la base de datos. Podemos agregar pimienta al código fuente como medida extra de seguridad.

#### Extensión

- PBKDF2
- bcrypt
- scrypt
- Argon2

En estos algoritmos lo que se busca es iterar el uso de distintos hashes y sales para demorar el proceso de obtención del hash de la contraseña, y de esta manera fortalecer nuestra aplicación contra ataques de fuerza bruta.

El ataque POODLE (del inglés "Padding Oracle On Downgraded Legacy Encryption") es relevante aquí. Para SSL 3.0 solo se necesitaban 256 solicitudes para revelar un byte de la comunicación. Este ataque aprovecha un mecanismo que reduce la seguridad con el fin de mantener interoperabilidad.

Para TLS 1.0 a 1.2, el ataque se basa en fallas en el cifrado CBC.

#### SSL Handshake

Se utiliza para establecer el método de encriptación que se va a mantener a lo largo de la comunicación y los datos de la sesión.

1. Contacto y establecimiento de capacidades:
    - RSA
    - Diffie-Hellman Autenticado
    - Diffie-Hellman Anónimo
    - Fortezza
2. Intercambio de llaves y autenticación del servidor
3. Intercambio de llaves y autenticación del cliente
4. Finalización del protocolo (aquí se crean las llaves de sesión)

#### SSL Récord

Se utiliza para transmitir información entre cliente y servidor.

1. Datos del mensaje
2. Fragmentación del mensaje
3. Compresión de los fragmentos
4. Agregado de un código de autenticación de mensaje
5. Cifrado de los datos
6. Agregado de un encabezado
7. Envío del criptograma a través de TCP

#### File Transfer Protocol

No contiene ninguna capa de seguridad.

#### File Transfer Protocol / SSL:

Es el mismo protocolo FTP pero sobre el protocolo SSL (actualmente TLS).

#### SSH File Transfer Protocol

Es un protocolo creado desde cero, muy diferente a FTP, que funciona basado en SSH.

#### Secure Copy Protocol

Se basa en:
- SSH
- FTP
- Comandos RCP
