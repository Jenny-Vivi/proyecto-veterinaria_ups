
# Actividad 2: Mapa de Navegación y Bocetos (Wireframes)

## 1. Introducción y propósito

El diseño de la interfaz y la experiencia de usuario (UI/UX) para el sistema web de **Vet San Francisco** se estructura en función de tres perfiles de usuario bien diferenciados: **Visitante**, **Cliente** y **Administrador**. Esto garantiza que cada actor acceda exclusivamente a las funciones autorizadas, asegurando una navegación intuitiva y evitando conflictos o solapamientos en el agendamiento de citas médicas y estéticas.

---

## 2. Mapa de navegación general

El flujo de pantallas y transiciones dentro de la plataforma web se organiza de la siguiente manera:

```text
[ Visitante (Anónimo) ]
  ├── Inicio / Home (Presentación corporativa de Vet San Francisco)
  ├── Catálogo de Servicios (Visualización de precios, duración y especialistas)
  ├── Iniciar Sesión (Formulario de autenticación)
  └── Registro de Usuario Nuevo (Creación de cuenta de cliente)

[ Cliente Autenticado ]
  ├── Panel de Cliente / Inicio
  ├── Módulo de Agendamiento de Citas
  │     ├── 1. Selección de Servicio (Consulta, Ecografía, Cirugía, Grooming)
  │     ├── 2. Selección de Especialista (Dra. Nicol Gómez o Dra. Marcela Chuchuca)
  │     ├── 3. Selección de Fecha y Bloque Horario Disponible (Lunes a Sábado, 08:00–21:00)
  │     └── 4. Confirmación de Reserva
  └── Mis Reservas (Historial de citas activas con opción de cancelación)

[ Administrador Autenticado ]
  ├── Panel de Administración (Dashboard General)
  ├── Gestión de Catálogo (Creación, edición y activación/desactivación de servicios)
  ├── Gestión de Recursos (Control de disponibilidad y turnos de las doctoras)
  └── Gestión de Citas Globales (Visualización de la agenda clínica y cambio de estado a Atendida/Cancelada)
```

---

## 3. Bocetos estructurales por pantalla

### Pantalla 01: Home / Página de inicio

**Propósito:** Recibir al usuario, presentar la identidad de Vet San Francisco y facilitar el acceso rápido a los servicios o al agendamiento.

**Boceto de interfaz:**

```text
+-----------------------------------------------------------------------+
| [LOGO] Vet San Francisco      Inicio | Servicios | Ingresar | Registro|
+-----------------------------------------------------------------------+
|                                                                       |
|   BIENVENIDOS A VET SAN FRANCISCO                                     |
|   Cuidado integral para especies mayores y menores en Cuenca.          |
|   Horario: Lunes a sábado de 08:00 a 21:00                            |
|                                                                       |
|   [ Botón: Agendar cita ahora ]   [ Botón: Ver servicios ]            |
|                                                                       |
+-----------------------------------------------------------------------+
|  Nuestras especialistas:                                              |
|  [ Dra. Nicol Gómez ]               [ Dra. Marcela Chuchuca ]         |
+-----------------------------------------------------------------------+
|  © 2026 Vet San Francisco - Cuenca, Ecuador                           |
+-----------------------------------------------------------------------+
```

### Pantalla 02: Catálogo de servicios

**Propósito:** Informar al usuario sobre los seis servicios parametrizados de la clínica, con sus tiempos y tarifas base.

**Boceto de interfaz:**

```text
+-----------------------------------------------------------------------+
| [LOGO] Vet San Francisco      Inicio | Servicios | Ingresar | Registro|
+-----------------------------------------------------------------------+
|  CATÁLOGO DE SERVICIOS Y TARIFAS                                     |
|                                                                       |
|  +-----------------------+  +-----------------------+  +--------------+|
|  | Consulta General      |  | Consulta Especialidad |  | Ecografía    ||
|  | Duración: 15 min     |  | Duración: 15 min      |  | Duración:    ||
|  | Precio: $15.00       |  | Precio: $20.00        |  | 10 min       ||
|  | [ Agendar ]          |  | [ Agendar ]           |  | Precio: $40  ||
|  +-----------------------+  +-----------------------+  +--------------+|
|                                                                       |
|  +-----------------------+  +-----------------------+  +--------------+|
|  | Esterilización macho |  | Esterilización hembra |  | Grooming     ||
|  | Duración: 30 min     |  | Duración: 60 min      |  | Duración:    ||
|  | Desde: $50.00        |  | Desde: $80.00         |  | 60 min       ||
|  | [ Agendar ]          |  | [ Agendar ]           |  | Desde: $13   ||
|  +-----------------------+  +-----------------------+  +--------------+|
+-----------------------------------------------------------------------+
```

### Pantalla 03: Inicio de sesión (Login) y registro

**Propósito:** Autenticar a clientes y administradores mediante Firebase Authentication.

**Boceto de interfaz:**

```text
+-----------------------------------------------------------------------+
| [LOGO] Vet San Francisco                             Volver al inicio |
+-----------------------------------------------------------------------+
|                                                                       |
|                  +---------------------------------+                  |
|                  |         INICIAR SESIÓN          |                  |
|                  |                                 |                  |
|                  |  Correo electrónico:            |                  |
|                  |  [___________________________]   |                  |
|                  |                                 |                  |
|                  |  Contraseña:                    |                  |
|                  |  [___________________________]   |                  |
|                  |                                 |                  |
|                  |      [     Ingresar     ]       |                  |
|                  |                                 |                  |
|                  |  ¿No tienes cuenta? Regístrate  |                  |
|                  +---------------------------------+                  |
|                                                                       |
+-----------------------------------------------------------------------+
```

### Pantalla 04: Módulo de agendamiento de citas (núcleo del sistema)

**Propósito:** Permitir al cliente autenticado reservar un bloque horario disponible sin cruces de agenda.

**Boceto de interfaz:**

```text
+-----------------------------------------------------------------------+
| [LOGO] Vet San Francisco     Agendar cita | Mis reservas | Salir (👤)|
+-----------------------------------------------------------------------+
|  NUEVA RESERVA DE CITA                                                 |
|                                                                       |
|  1. Seleccione el servicio:   [ v Consulta General (15 min - $15) ]   |
|  2. Seleccione especialista:  [ v Dra. Nicol Gómez                ]   |
|  3. Seleccione la fecha:      [ 📅 2026-11-28                     ]   |
|                                                                       |
|  4. Horarios disponibles (bloques libres sin solapamiento):           |
|     [ 08:00 ] [ 08:15 ] [ 08:30 ] [ 09:00 ] [ 09:15 ] [ 10:00 ]      |
|     [ 10:30 ] [ 11:00 ] [ 14:00 ] [ 14:30 ] [ 15:00 ] [ 16:00 ]      |
|                                                                       |
|  Resumen: Consulta General con Dra. Nicol Gómez el 28/11 a las 09:00  |
|                                                                       |
|                      [ Confirmar reserva ]                            |
+-----------------------------------------------------------------------+
```

**Nota:** La fecha y los horarios mostrados son ejemplos de diseño. En el sistema real, deben generarse según la disponibilidad configurada y las citas existentes.

### Pantalla 05: Panel de «Mis reservas» (vista del cliente)

**Propósito:** Mostrar al cliente sus citas programadas e historial, permitiéndole cancelar reservas futuras confirmadas.

**Boceto de interfaz:**

```text
+-----------------------------------------------------------------------+
| [LOGO] Vet San Francisco     Agendar cita | Mis reservas | Salir (👤)|
+-----------------------------------------------------------------------+
|  MIS CITAS PROGRAMADAS                                                |
|                                                                       |
|  +-----------------------------------------------------------------+  |
|  | Servicio        | Especialista       | Fecha y hora | Estado     |  |
|  +-----------------------------------------------------------------+  |
|  | Consulta Gral.  | Dra. Nicol Gómez   | 28/11 09:00  | CONFIRMADA |  |
|  |                 |                    |              | [Cancelar] |  |
|  +-----------------------------------------------------------------+  |
|  | Grooming        | Dra. M. Chuchuca   | 15/11 10:00  | ATENDIDA   |  |
|  +-----------------------------------------------------------------+  |
|  | Ecografía       | Dra. Nicol Gómez   | 10/11 16:00  | CANCELADA  |  |
|  +-----------------------------------------------------------------+  |
+-----------------------------------------------------------------------+
```

### Pantalla 06: Panel de administración (dashboard global)

**Propósito:** Permitir al administrador gestionar servicios, horarios de las doctoras y supervisar todas las citas de la clínica.

**Boceto de interfaz:**

```text
+-----------------------------------------------------------------------+
| [LOGO] Vet San Francisco [ADMIN]       Servicios | Recursos | Agenda  |
+-----------------------------------------------------------------------+
|  GESTIÓN DE AGENDA GLOBAL DE LA CLÍNICA                               |
|  Filtrar por doctora: [ Todas v ]    Filtrar por fecha: [28/11/2026] |
|                                                                       |
|  +-----------------------------------------------------------------+  |
|  | Cliente      | Servicio       | Doctora       | Hora  | Acciones |  |
|  +-----------------------------------------------------------------+  |
|  | Juan Pérez   | Consulta Gral. | Dra. N. Gómez  | 09:00 | [Atender]|  |
|  |              |                |               |       | [Cancelar]|  |
|  +-----------------------------------------------------------------+  |
|  | María López  | Esteril. Hembra| Dra. Chuchuca | 10:00 | [Atender]|  |
|  |              |                |               |       | [Cancelar]|  |
|  +-----------------------------------------------------------------+  |
|                                                                       |
|  [ + Nuevo servicio ]   [ Configurar horarios de turno ]              |
+-----------------------------------------------------------------------+
```
