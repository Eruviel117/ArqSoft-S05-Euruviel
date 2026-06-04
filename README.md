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

---

##  Capturas de pantalla

###  Apartado de inicio
> Donde se muestra el registro de Pacientes

<img width="1365" height="670" alt="Captura de pantalla 2026-06-04 173011" src="https://github.com/user-attachments/assets/684386be-fd32-4eb1-b387-6c4a46848c0e" />


###  Apartado de Médicos
> Donde se muestra el registro de Médicos disponibles

<img width="1365" height="684" alt="Captura de pantalla 2026-06-04 173022" src="https://github.com/user-attachments/assets/76fe27cb-80a7-4a84-a648-d7c4220a5990" />



###  Apartado de Citas
> Donde se muestra el registro de Citas agendadas 

<img width="1365" height="707" alt="Captura de pantalla 2026-06-04 173046" src="https://github.com/user-attachments/assets/23303735-b103-4956-9127-eb7f5a3f7c0e" />



---

## Declaración de uso de Inteligencia Artificial

| Campo | Detalle |
|---|---|
| **Nombre del estudiante** | Euruviel Marquez  |
| **IA utilizada** | Claude |
| **Fecha de uso** | 02/06/2026 |
| **Propósito** | Guía para estructurar el proyecto y corrección de errores |

### Prompts utilizados:
- *okey tengo este error en este proyecto puedes ayudarme a solucionarlo porfavor


### Respuesta en crudo (raw):

Veo el problema — ese archivo tiene el namespace CitasApp (sin guión bajo) pero tu proyecto es Citas_App. Reemplaza todo el contenido de PorPaciente.cshtml con esto:
html@model List<Citas_App.Models.Cita>
@using Citas_App.Models
@{
    ViewData["Title"] = "Citas por paciente";
    var pacientes = ViewBag.Pacientes as List<Paciente>;
    var medicos = ViewBag.Medicos as List<Medico>;
    var primero = Model.FirstOrDefault();
    var pac = pacientes?.FirstOrDefault(p => p.Id == primero?.PacienteId);
}

<div class="page-card">
    <a class="btn-back" asp-controller="Cita" asp-action="Index">← Ver todas las citas</a>
    <div class="d-flex align-items-center gap-2 mt-3 mb-3">
        <span class="page-title mb-0">
            Citas de @(pac != null ? $"{pac.Nombre} {pac.Apellido}" : "paciente")
        </span>
        <span class="badge-count">@Model.Count citas</span>
    </div>
    <table class="table">
        <thead>
            <tr>
                <th>Fecha</th>
                <th>Hora</th>
                <th>Médico</th>
                <th>Motivo</th>
                <th>Estado</th>
            </tr>
        </thead>
        <tbody>
        @foreach (var c in Model)
        {
            var medico = medicos?.FirstOrDefault(m => m.Id == c.MedicoId);
            <tr>
                <td>@c.Fecha.ToString("dd/MM/yyyy")</td>
                <td>@c.Hora.ToString("HH:mm")</td>
                <td>@(medico != null ? $"{medico.Nombre} {medico.Apellido}" : "—")</td>
                <td>@c.Motivo</td>
                <td><span class="status-@c.Estado.ToLower()">@c.Estado</span></td>
            </tr>
        }
        </tbody>
    </table>
</div>
El cambio clave es la primera línea: CitasApp.Models.Cita → Citas_App.Models.Cita y lo mismo con el @using. Ese namespace incorrecto es lo que causa los 3 errores que ves en la barra de abajo. ¿Se resuelven?
