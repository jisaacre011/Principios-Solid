<div align="center">
  <img src="https://raw.githubusercontent.com/jisaacre011/Principios-Solid/main/Portada%20.png" width="600">
</div>

# Principios SOLID: Comprensión, Análisis y Refactorización

## Objetivo

Comprender los principios SOLID, identificar problemas comunes en el código orientado a objetos y aplicar refactorización para mejorar la mantenibilidad, escalabilidad y claridad del software.

---

## 1. Investigación y análisis

### 1.1 ¿Qué significa SOLID?

SOLID es un acrónimo que agrupa cinco principios de diseño orientado a objetos. La idea de fondo es simple: escribir clases que hagan una sola cosa, que sean fáciles de extender y que dependan unas de otras lo menos posible.

- **S — Single Responsibility Principle (Responsabilidad Única):** una clase debe tener una sola razón para cambiar. Es decir, una sola responsabilidad.
- **O — Open/Closed Principle (Abierto/Cerrado):** el código debe estar abierto a extensión pero cerrado a modificación. Se agrega comportamiento nuevo sin tocar lo que ya funciona.
- **L — Liskov Substitution Principle (Sustitución de Liskov):** una clase hija debe poder usarse en lugar de su clase padre sin romper el programa.
- **I — Interface Segregation Principle (Segregación de Interfaces):** es mejor tener varias interfaces pequeñas y específicas que una sola grande que obligue a implementar cosas que no se usan.
- **D — Dependency Inversion Principle (Inversión de Dependencias):** el código debe depender de abstracciones (interfaces), no de implementaciones concretas.

### 1.2 ¿Por qué SOLID es importante en la POO?

**Cómo ayuda a mantener proyectos grandes**

En un proyecto pequeño casi cualquier diseño funciona. El problema aparece cuando hay miles de líneas y varias personas tocando el mismo código. SOLID mantiene las piezas **separadas y bien definidas**, así un cambio en un lugar no provoca fallos inesperados en otro. Es la diferencia entre una caja de herramientas ordenada y un cajón donde todo está revuelto.

**Qué problemas aparecen cuando no se usan estos principios**

- Clases enormes que hacen de todo y que nadie quiere tocar por miedo a romper algo.
- Un cambio pequeño obliga a modificar muchos archivos (**efecto dominó**).
- Código difícil de probar porque todo está conectado con todo.
- Duplicación de lógica porque reutilizar es complicado.
- Curva de aprendizaje alta para quien entra nuevo al proyecto.

**Cómo influye SOLID en:**

- **Mantenimiento:** los cambios quedan **localizados**. Si algo falla, sabes dónde buscar.
- **Reutilización:** las clases pequeñas y bien definidas se reaprovechan en otros contextos.
- **Escalabilidad:** agregar funciones nuevas no implica reescribir lo existente.
- **Pruebas:** al depender de abstracciones, puedes sustituir partes por versiones falsas (mocks) y **probar en aislamiento**.
- **Trabajo en equipo:** cada quien trabaja en su módulo sin pisarse con los demás.

---

<div style="page-break-before: always;"></div>

## 2. Conceptos clave

- **Acoplamiento:** qué tan amarradas están dos clases entre sí. Mucho acoplamiento significa que cambiar una obliga a cambiar la otra. Lo ideal es **acoplamiento bajo**, como electrodomésticos que funcionan con un enchufe estándar en lugar de estar soldados a la pared.
- **Cohesión:** qué tan enfocada está una clase en una sola tarea. **Alta cohesión** es bueno: la clase hace una cosa y la hace bien.
- **Refactorización:** mejorar la estructura interna del código **sin cambiar lo que hace** de cara al usuario. Es como reorganizar un cuarto: los muebles siguen siendo los mismos, pero ahora todo es más fácil de encontrar.
- **Escalabilidad:** la capacidad del sistema de **crecer** (más usuarios, más funciones) sin que haya que reconstruirlo desde cero.
- **Mantenibilidad:** qué tan fácil es **entender, corregir y modificar** el código con el paso del tiempo.
- **Abstracción:** quedarse con lo esencial y **ocultar el detalle**. Un volante abstrae todo el mecanismo de dirección: lo giras y el carro dobla, sin que te importe cómo.
- **Dependencias:** las otras clases o módulos que una clase necesita para funcionar. Mientras **menos y más abstractas** sean, mejor.

---

<div style="page-break-before: always;"></div>

## 3. Práctica: Refactorización guiada

### Parte 1 — Principio S (SRP)

**Código original:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20S,%20Codigo%20Malo.png?raw=true" width="500">
</div>

La clase original mezcla tres trabajos distintos: generar el reporte, guardarlo y enviarlo por correo. Si cambia la forma de enviar correos, hay que tocar la misma clase que genera reportes, lo cual no tiene sentido.

**Código corregido:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20S,%20Codigo%20Corregido.png?raw=true" width="650">
</div>

<div style="page-break-before: always;"></div>

**¿Qué problema tenía el diseño original?**
Una sola clase tenía **tres razones para cambiar**. Cualquier ajuste en el guardado, en el correo o en la generación afectaba la misma clase, aumentando el riesgo de errores.

**¿Qué ventajas aporta la refactorización?**
Cada clase tiene un **único propósito**, es más fácil de leer, de **probar y de reutilizar**. Cambiar el envío de correo **ya no toca el código de generación**.

**¿Qué ocurriría si el sistema crece?**
Con el diseño original la clase se volvería un **monstruo inmanejable**. Con la separación, se agregan o modifican comportamientos de forma independiente, por ejemplo guardar también en la nube sin tocar nada más.

---

<div style="page-break-before: always;"></div>

### Parte 2 — Principio O (OCP)

**Código original:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20O,%20Codigo%20Malo.png?raw=true" width="500">
</div>

El problema del código original es la cadena de `if`: cada cliente nuevo obliga a editar el método `Calcular`. La solución es definir una interfaz y una clase por cada tipo de descuento.

**Código corregido:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20O,%20Codigo%20Corrigido.png?raw=true" width="500">
</div>

**¿Por qué este código no es escalable?**
Porque cada tipo de cliente nuevo obliga a **abrir una clase que ya estaba probada** y funcionando, con el riesgo de romper lo anterior. La cadena de `if` crece sin control.

**¿Cómo ayuda el polimorfismo?**
Permite que la calculadora trabaje con **cualquier objeto que cumpla la interfaz** `IDescuento`, sin saber ni importarle de qué tipo concreto se trata. Cada clase sabe calcular su propio descuento.

**¿Qué ventaja ofrece OCP en proyectos grandes?**
El código existente se **mantiene estable**. Las funciones nuevas se agregan en archivos nuevos, lo que reduce el riesgo de introducir errores en partes que ya funcionaban.

---

<div style="page-break-before: always;"></div>

### Parte 3 — Principio L (LSP)

**Código original:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20L,%20Codigo%20Malo.png?raw=true" width="500">
</div>

El pingüino es un ave pero no vuela, así que heredar de una clase `Ave` que asume el vuelo genera un comportamiento inválido. La solución es separar la capacidad de volar en su propia interfaz, en lugar de imponerla a todas las aves.

**Código corregido:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20L,%20Codigo%20Corregido.png?raw=true" width="500">
</div>

**¿Por qué el pingüino viola LSP?**
Porque al sustituir un `Ave` por un `Pinguino`, el programa **se rompe**: llamar a `Volar()` lanza una excepción. La clase hija no se comporta como promete la clase padre.

**¿Qué riesgos genera esto?**
**Errores en tiempo de ejecución** difíciles de prever, código defensivo lleno de validaciones de tipo, y pérdida de confianza en las jerarquías de herencia.

**¿Cómo mejorarías la jerarquía?**
Separando capacidades en interfaces (`IVolador`, `INadador`, etc.) y dejando que cada clase implemente **solo las que realmente puede cumplir**, en vez de forzar comportamientos a través de la herencia.

---

<div style="page-break-before: always;"></div>

### Parte 4 — Principio I (ISP)

**Código original:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20I,%20Codigo%20Malo.png?raw=true" width="500">
</div>

La interfaz `ITrabajador` obliga al robot a implementar `Comer()`, algo que no tiene sentido. La solución es dividir la interfaz grande en interfaces pequeñas y específicas.

**Código corregido:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20I,%20Codigo%20Corregido.png?raw=true" width="500">
</div>

**¿Qué problema presenta esta interfaz?**
Obliga a las clases a **implementar métodos que no necesitan**. El robot termina con un `Comer()` que solo lanza una excepción, lo cual es código muerto y peligroso.

**¿Cómo mejora ISP el diseño?**
Cada clase implementa **únicamente lo que le corresponde**. No quedan métodos vacíos ni excepciones forzadas, y el contrato de cada interfaz es honesto.

**¿Qué ventajas ofrece dividir interfaces?**
Mayor **flexibilidad** para combinar capacidades, menos código inútil, y mayor claridad sobre qué puede hacer realmente cada clase.

---

<div style="page-break-before: always;"></div>

### Parte 5 — Principio D (DIP)

**Código original:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20D,%20Codigo%20Malo.png?raw=true" width="500">
</div>

`UsuarioService` crea directamente una `MySQLDatabase`, lo que lo amarra a esa base de datos. La solución es depender de una interfaz e inyectar la implementación desde fuera.

**Código corregido:**
<div align="center">
  <img src="https://github.com/jisaacre011/Principios-Solid/blob/main/Principio%20D,%20Codigo%20Corregido.png?raw=true" width="500">
</div>

**¿Por qué el acoplamiento es un problema?**
Porque amarra el servicio a una **tecnología concreta**. Cambiar de MySQL a otra base de datos obligaría a modificar el código del servicio, y probarlo sin una base de datos real sería casi imposible.

**¿Qué ventajas ofrece depender de abstracciones?**
El servicio funciona con **cualquier base de datos** que cumpla la interfaz `IBaseDatos`. Se pueden intercambiar implementaciones sin tocar la lógica del servicio.

**¿Cómo ayuda DIP en pruebas unitarias?**
Permite inyectar una **base de datos falsa (mock)** durante las pruebas, de modo que se puede probar la lógica de `UsuarioService` sin conectarse a una base de datos real, lo que hace las pruebas rápidas y confiables.

---

<div style="page-break-before: always;"></div>

## 4. Reflexión final

**¿Cuál principio SOLID consideras más difícil?**
El de **Inversión de Dependencias (D)**. Al principio cuesta acostumbrarse a no crear los objetos directamente con `new` dentro de las clases. La idea de que algo externo decida qué implementación usar se siente extraña hasta que se entiende el beneficio para las pruebas y el mantenimiento.

**¿Cuál crees que aporta más valor?**
El de **Responsabilidad Única (S)**. Es la base de todos los demás: cuando cada clase hace una sola cosa, casi automáticamente el código se vuelve más fácil de extender, de probar y de mantener. Es el principio que más impacto tiene con menos esfuerzo.

**¿Cómo cambiaría tu manera de programar después de esta actividad?**
Ahora pienso primero en **separar responsabilidades** antes de escribir una clase, y me detengo a preguntarme si lo que estoy haciendo me obligará a modificar código existente en el futuro. También presto más atención a depender de interfaces en lugar de clases concretas.

**¿Qué diferencias notas entre un código rápido y un código bien diseñado?**
El código rápido **funciona hoy pero se vuelve una carga mañana**: todo está mezclado, cualquier cambio da miedo y probarlo es un dolor de cabeza. El código bien diseñado toma un poco más de tiempo al inicio, pero **crece sin romperse**, se entiende a simple vista y permite que varias personas trabajen sin pisarse. La inversión inicial se paga sola con el tiempo.