# Lector de crotales

Propuesta de una aplicación móvil para consultar y gestionar la identificación del ganado mediante la lectura de crotales con la cámara del teléfono.

> **Estado del proyecto:** fase de planteamiento. Las funciones descritas en este documento son objetivos del proyecto; todavía no implican que estén implementadas.

## Objetivo

Facilitar el trabajo diario de las ganaderías: leer el crotal de un animal con la cámara, localizar su registro y permitir a las personas autorizadas añadir animales o tramitar su baja. La aplicación también contempla un espacio de consulta para el Estado y el intercambio de información mediante archivos CSV, sin compartir directamente las bases de datos internas.

## Enfoque de la aplicación

El diseño partirá de las necesidades de las personas que la utilizarán en el trabajo diario, especialmente ganaderos y trabajadores. Las tareas frecuentes deberán ser claras y rápidas desde un móvil: abrir la cámara, comprobar el crotal leído y consultar o actualizar el registro según los permisos.

La primera versión se plantea como una aplicación web adaptable a móviles. La arquitectura deberá permitir que, en una fase futura, esa misma aplicación se empaquete como una aplicación móvil instalable, por ejemplo como APK para Android, sin tener que rehacer todo el producto. La interfaz móvil se comunicará con un servidor mediante una API; el servidor aplicará los permisos y gestionará la base de datos.

```text
Aplicación web móvil (futura APK) → API → servidor → base de datos
```

El empaquetado como APK queda previsto para el futuro y no forma parte de la primera entrega. Antes de decidir la tecnología definitiva habrá que probar el acceso a la cámara y la lectura de crotales en los dispositivos que se usarán en las ganaderías.

## Funcionamiento previsto

1. La persona usuaria abre la cámara desde la aplicación y enfoca el crotal.
2. La aplicación detecta la zona del crotal y trata de leer su identificador.
3. La pantalla resalta la zona detectada con un recuadro translúcido y atenúa ligeramente el resto de la imagen.
4. Antes de realizar una acción, se muestra el identificador leído para que pueda comprobarse y corregirse si hace falta.
5. Según los permisos de la cuenta, se consulta el registro, se añade un animal o se inicia su baja.

La lectura automática deberá poder corregirse manualmente. Una detección errónea no debería provocar por sí sola una modificación o eliminación de datos.

## Perfiles y permisos

- **Superadministrador:** administra la plataforma, las cuentas y la configuración general.
- **Ganadería:** gestiona los registros de su propia explotación y las cuentas de sus trabajadores.
- **Trabajador:** realiza las tareas que le autorice su ganadería, como consultar crotales o registrar altas y bajas.
- **Estado:** dispone de acceso de solo lectura en la aplicación. En la primera versión planteada, consulta una tabla con el identificador del crotal y la ganadería correspondiente.

Los datos de cada ganadería deben quedar aislados: sus usuarios no deben poder consultar los registros de otras explotaciones. El perfil del Estado tampoco tendrá permisos para modificar datos desde la aplicación.

## Intercambio con el Estado

La propuesta contempla que la ganadería y el Estado mantengan sus propias bases de datos, sin acceso directo de una parte a la base interna de la otra. El intercambio se realizaría mediante archivos CSV. Desde la aplicación, el Estado solo consultaría la información autorizada que se muestre en su tabla.

Queda por acordar el formato exacto del CSV, qué campos incluirá, quién podrá generarlo y cómo se validarán los datos antes de incorporarlos a cada sistema.

## Gestión de animales

La aplicación deberá contemplar, como mínimo:

- Consultar un animal a partir de su crotal.
- Añadir un animal y asociarlo a una ganadería.
- Registrar una baja con los permisos correspondientes.
- Evitar cambios accidentales mediante una comprobación del identificador y una confirmación de la acción.

Está pendiente decidir si una baja será definitiva o si el registro se conservará marcado como inactivo, así como qué información adicional se guardará de cada animal.

## Decisiones pendientes

- Tecnología de reconocimiento adecuada para los crotales utilizados y condiciones reales de lectura.
- Campos que compondrán el registro de cada animal y de cada ganadería.
- Permisos concretos de superadministradores, ganaderías y trabajadores.
- Formato, flujo y validación de los archivos CSV.
- Comportamiento con poca cobertura y sincronización de cambios.
- Tecnología para empaquetar la aplicación web como app móvil instalable.
- Política de conservación, privacidad, seguridad y trazabilidad de las modificaciones.

## Alcance inicial

La primera versión se centrará en una app móvil para las ganaderías, la lectura asistida del crotal, la gestión de altas y bajas con permisos y una vista de consulta de solo lectura para el Estado con las columnas **crotal** y **ganadería**. La integración automática con sistemas externos del Estado no forma parte del alcance inicial; el intercambio se plantea mediante CSV.
