# Tecnológico de Software
- **Arquitectura de Software**
- **Alumno:** Euruviel Marquez Martinez
- **Docente:** Jorge Javier Pedrozo Romero
- **Fecha:** 04/06/2026
- **Actividad:** Actividad #14 – Práctica .NET: Implementar MVC con ASP.NET Core

---

## Descripción

**CitasMédicas** es una aplicación web desarrollada con **ASP.NET Core MVC** que permite gestionar un sistema de citas médicas. Permite visualizar pacientes registrados, médicos disponibles y la agenda completa de citas, con filtro por paciente.

El proyecto aplica el patrón **repositorio con interfaces**, separando la lógica de acceso a datos de los controladores mediante inyección de dependencias.

---

## Arquitectura

El proyecto sigue una estructura **MVC con capa de repositorios**:

```

Citas_App/
├── Controllers/
│   ├── HomeController.cs
│   ├── PacienteController.cs
│   ├── MedicoController.cs
│   └── CitaController.cs
│
├── Interfaces/
│   ├── IPacienteRepository.cs
│   ├── IMedicoRepository.cs
│   └── ICitaRepository.cs
│
├── Repositories/
│   ├── JsonPacienteRepository.cs
│   ├── JsonMedicoRepository.cs
│   └── JsonCitaRepository.cs
│
├── Models/
│   ├── Paciente.cs
│   ├── Medico.cs
│   ├── Cita.cs
│   └── CitaJson.cs
│
├── Views/
│   ├── Paciente/
│   │   ├── Index.cshtml
│   │   └── Detalle.cshtml
│   ├── Medico/
│   │   ├── Index.cshtml
│   │   └── Detalle.cshtml
│   └── Cita/
│       ├── Index.cshtml
│       └── PorPaciente.cshtml
│
└── data/
    ├── pacientes.json
    ├── medicos.json
    └── citas.json

```


---

## Funcionalidades

| Funcionalidad | Descripción |
|---|---|
| Lista de pacientes | Tabla con nombre, email y teléfono de cada paciente |
| Detalle de paciente | Información completa con link a sus citas |
| Lista de médicos | Tabla con nombre, especialidad y número de licencia |
| Detalle de médico | Información completa del médico |
| Agenda de citas | Tabla con fecha, hora, paciente, médico, motivo y estado |
| Citas por paciente | Filtro de citas de un paciente específico |
| Estadísticas | Contador de citas totales, pendientes y confirmadas |
| Navbar global | Navegación entre secciones desde cualquier página |

---

## Tecnologías utilizadas

| Tecnología | Versión | Uso |
|---|---|---|
| C# | 13 | Lenguaje principal |
| ASP.NET Core MVC | .NET 10 | Framework web |
| JSON | — | Persistencia de datos |
| Git + GitHub | — | Control de versiones |

---

## Persistencia de datos

Los datos se almacenan en archivos **JSON** dentro de la carpeta `data/`:

| Archivo | Contenido |
|---|---|
| `pacientes.json` | Pacientes registrados en el sistema |
| `medicos.json` | Médicos disponibles con especialidad y licencia |
| `citas.json` | Agenda de citas con estado y motivo |

---

## Patrones y principios aplicados

| Principio | Aplicación |
|---|---|
| **Patrón Repositorio** | Interfaces `IPacienteRepository`, `IMedicoRepository`, `ICitaRepository` desacoplan el acceso a datos |
| **Inyección de dependencias** | Repositorios registrados en `Program.cs` como `AddScoped` |
| **SRP** — Single Responsibility | Cada controller maneja una sola entidad |
| **MVC** | Separación clara entre Modelos, Vistas y Controladores |
| **DIP** — Dependency Inversion | Los controllers dependen de interfaces, no de implementaciones concretas |

---

## Vistas arquitectónicas

| Vista | Descripción |
|---|---|
| **Lógica** | Módulos: Gestión de Pacientes, Gestión de Médicos, Gestión de Citas |
| **Desarrollo** | Estructura MVC con carpetas Controllers, Interfaces, Repositories, Models, Views |
| **Procesos** | Petición HTTP → Controller → Repository → JSON → View |

