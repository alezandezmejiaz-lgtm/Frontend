# AGENTS.md — Licorería Junín Currinchero

## Instrucciones específicas de este repositorio: Frontend

**Repositorio:** https://github.com/alezandezmejiaz-lgtm/Frontend.git

**Responsable principal:** AG-004 (frontend). AG-003 diseña interfaz; AG-001 verifica RF/RNF; AG-006 prueba; AG-007 coordina; AG-005 acuerda contratos API.

**Ámbito permitido:** aplicación de Usuario para Android y web con Ionic, Angular, TypeScript, Capacitor y estilos. Implementar solo las vistas y funcionalidades asignadas a Usuario y autenticación compartida según DERCAS. iOS no es entrega inicial confirmada.

**Asistentes integrados:** AAC-001 en catálogo/búsqueda, AAC-002 en seguimiento de pedidos propios y AAC-003 en ayuda/contacto, dentro de vistas existentes. Consumir exclusivamente endpoints autorizados del Backend; nunca usar credenciales de MySQL ni claves secretas en el cliente. No asumir datos de precios, stock ni estados de pedidos.

**Marca:** respetar el logo oficial y la paleta de la sección 6.1, con contraste, legibilidad y accesibilidad. Utilizar prototipos Figma aprobados cuando existan; no inventar enlaces ni afirmar que están aprobados.

**Límites:** no crear un tercer rol Cliente; no implementar pantallas administrativas en este repositorio salvo aprobación explícita de alcance; no validar pagos solo por comprobante. Coordinar con Backend antes de cambiar contratos API.

**Verificación previa a revisión:** ejecutar compilación, lint y pruebas únicamente si existen scripts configurados; comprobar navegación, responsive, validación, accesibilidad y manejo de errores. Reportar evidencias y limitaciones. Commit y push solo tras las autorizaciones correspondientes de la sección 11.

---


> **Estado:** instrucciones propuestas para el desarrollo asistido por IA. Este archivo no demuestra que los agentes estén instalados, conectados o ejecutándose. Debe validarse frente a las versiones aprobadas de la propuesta y DERCAS.

## 1. Propósito y fuentes de verdad

Desarrollar una aplicación multiplataforma (móvil y web) para Licorería Junín Currinchero mediante agentes de IA coordinados, con supervisión humana, trazabilidad y ciclos de revisión y corrección.

**Orden de referencia:**
1. `docs/Propuesta_y_DERCAS_Licoreria_Junin_Currinchero_Completado.pdf`: **Parte I: Propuesta** y **Parte II: DERCAS aplicado**, en ese orden. Es la referencia documental integrada; comprobar aprobación humana de la versión.
2. `docs/diagramas/arquitectura-por-capas.png`, `docs/diagramas/arquitectura-con-ia.png` y `docs/diagramas/modelo-entidad-relacion.png`: referencias gráficas del proyecto, sujetas a cotejo con el documento.
3. Versiones efectivamente aprobadas de FigJam, Figma, contratos API y código fuente. No suponer enlaces ni conexiones existentes.

Las rutas indicadas existen en el paquete de referencias adjunto; para cada repositorio, copiar la carpeta `docs/` junto a `AGENTS.md` o garantizar que sus rutas relativas sean accesibles. La existencia de los archivos **no acredita aprobación académica**. Si hay discrepancias, registrar hallazgo y solicitar decisión humana; no alterar silenciosamente el alcance.

### 1.1. Contexto del proyecto y referencia obligatoria al DERCAS

**Proyecto:** Licorería Junín Currinchero, aplicación multiplataforma para Android y navegadores web, con backend organizado en cinco capas.

**Documento rector del contexto (PDF incluido en este paquete):** `docs/Propuesta_y_DERCAS_Licoreria_Junin_Currinchero_Completado.pdf`. Consultar **primero la Parte I (Propuesta de proyecto de software)** para conocer el problema, alcance, módulos, arquitectura, tecnologías y modelo de datos; consultar **después la Parte II (DERCAS aplicado)** para identificar requerimientos, criterios de aceptación, responsabilidades de agentes, trazabilidad y ciclos de revisión y corrección. No tratar el DERCAS como documentación opcional.

**Aplicación del DERCAS a cada tarea:** antes de analizar, diseñar, programar o probar, AG-001 a AG-007 deben identificar los códigos RF/RNF pertinentes, sus criterios de aceptación y las restricciones documentadas. Registrar en cada tarea `fuentes_aprobadas`, los requisitos relacionados y la evidencia prevista. Ante diferencias entre propuesta, DERCAS y diagramas, detener el cambio afectado, documentar la discrepancia y solicitar validación humana; no inventar requisitos ni resolver contradicciones unilateralmente.

**Referencias visuales complementarias:** `docs/diagramas/arquitectura-por-capas.png` (cinco capas y tecnologías), `docs/diagramas/arquitectura-con-ia.png` (AAC-001 a AAC-003 y límites de acceso) y `docs/diagramas/modelo-entidad-relacion.png` (modelo gráfico de 21 tablas). Estos archivos están incluidos en el paquete; comprobar siempre que correspondan a la versión aprobada. Las imágenes explican el diseño, pero no sustituyen los requisitos y criterios del DERCAS.

**Regla de actualización:** cualquier modificación de alcance, roles, vistas, tablas, RF/RNF, flujos de pago o permisos requiere solicitud de cambio y aprobación humana antes de actualizar el código o los documentos. La ruta documental es la propuesta en el repositorio; verificar su existencia antes de usarla.

## 2. Alcance obligatorio

- Aplicación móvil Android y web para computadoras con Ionic, Angular, TypeScript y Capacitor. iOS es posibilidad futura, no entrega inicial confirmada.
- Backend Node.js + Express.js; API REST, autenticación JWT, autorización por roles (RBAC), validación de entradas y limitación de solicitudes.
- Lógica de negocio en servicios; acceso a datos mediante repositorios/modelos Sequelize; persistencia MySQL.
- Exactamente **dos roles**: `Administrador` y `Usuario`. «Cliente» es el área funcional de Usuario, no un tercer rol.
- Mantener **21 vistas principales**, **21 tablas** del modelo propuesto, **RF-001 a RF-255** y **RNF-001 a RNF-072**, salvo cambio formal aprobado.
- La aplicación cubre catálogo, búsqueda y filtros, carrito, pedidos, seguimiento, historial, perfil, notificaciones, ayuda, productos, categorías, inventario, ventas, clientes, usuarios y permisos, reportes, configuración y atención al cliente.
- El administrador controla el stock mínimo, entradas/salidas y alertas de existencias.
- Los pagos previstos son efectivo y transferencia mediante banca móvil, con **verificación administrativa manual**.
- La compra y entrega de bebidas alcohólicas requiere los controles legales y de mayoría de edad que se definan y validen para el despliegue.

## 3. Asistentes de IA integrados en la aplicación

Estos asistentes **no son los agentes que programan** el sistema. Se incorporan a vistas existentes, sin añadir un rol ni una vista principal:

| Código | Vista existente | Función | Restricción |
|---|---|---|---|
| AAC-001 | Catálogo y búsqueda | Consultar productos, precios, categorías y disponibilidad | Solo datos autorizados y vigentes desde API |
| AAC-002 | Seguimiento de pedidos | Informar estado de pedidos propios | Exige sesión y verificación de titularidad en backend |
| AAC-003 | Ayuda y contacto | Preguntas frecuentes y derivación humana | Solo políticas aprobadas; reconocer límites |

Los AAC no tienen acceso directo a MySQL ni permisos para cambiar pedidos, aprobar pagos, realizar compras o modificar inventario.

## 4. Arquitectura obligatoria: cinco capas

1. **Presentación:** Ionic + Angular + TypeScript + Capacitor; interfaz móvil y web responsive, incluidas vistas con AAC.
2. **Controladores y API REST:** Node.js + Express; rutas, controladores, JWT, RBAC, validación y rate limiting.
3. **Lógica de negocio:** servicios de pedidos, inventario, ventas, pagos, atención y servicios de IA con reglas de negocio.
4. **Acceso a datos:** Sequelize ORM, modelos y repositorios; consultas filtradas por permisos y titularidad.
5. **Persistencia:** MySQL, 21 tablas del modelo aprobado, integridad referencial y transacciones.

Flujo: `Ionic/Angular → API Express → servicios → Sequelize → MySQL`.

Consultar las imágenes aprobadas en `docs/diagramas/` (ruta sugerida). No interpretar el diagrama como autorización para saltarse capas.

## 5. Herramientas, finalidad y agentes responsables

| Tecnología/herramienta | Uso previsto | Agente responsable |
|---|---|---|
| Ionic + Angular + TypeScript | Desarrollo de interfaz móvil y web | AG-004 |
| Capacitor | Empaquetado y acceso controlado a funciones móviles | AG-004 |
| HTML / SCSS | Estructura y estilos de las interfaces | AG-003 / AG-004 |
| Node.js + Express.js | API REST, rutas, controladores y middleware | AG-005 |
| JWT + RBAC | Autenticación y autorización, verificadas en backend | AG-005 / AG-006 |
| Sequelize | ORM, modelos, relaciones y consultas | AG-005 |
| MySQL | Persistencia relacional y transacciones | AG-005 |
| Figma | Wireframes, diseño UI/UX y prototipos móvil/escritorio | AG-003 |
| FigJam | Casos de uso, diagramas UML, actividades y flujos | AG-002 |
| dbdiagram.io | Diagrama entidad-relación del modelo de 21 tablas | AG-002 / AG-005 |
| Git | Control local de versiones y un commit por cambio lógico aprobado | AG-001 a AG-007 / AG-007 supervisa |
| GitHub | Repositorios remotos, ramas, pull requests, revisión y trazabilidad | AG-007 / equipo humano |
| OpenCode | Configuración y ejecución de agentes de desarrollo, cuando estén instalados y habilitados | AG-001 a AG-007 |
| Codex | Implementación y revisión de código, según acceso disponible | AG-004 / AG-005 / AG-006 |
| Claude | Revisión independiente de requisitos, arquitectura y código, según acceso disponible | AG-001 / AG-006 |
| ChatGPT | Análisis de requisitos, planificación y coordinación, según acceso disponible | AG-001 / AG-007 |

### 5.1. Reglas de utilización de herramientas

1. Antes de iniciar una tarea, cada agente deberá consultar este `AGENTS.md`, la propuesta del proyecto y DERCAS, cuando esos documentos estén disponibles en las rutas indicadas en la sección 1. Si falta una fuente, reportarlo y solicitarla; no inventar contenido.
2. Cada agente utilizará únicamente las tecnologías, archivos y acciones autorizados para su responsabilidad y para la tarea asignada.
3. AG-007 coordinará la asignación de tareas, comprobará dependencias, registrará revisiones y solicitará aprobación humana cuando corresponda.
4. AG-002 y AG-003 deberán respetar los diagramas UML y prototipos aprobados en FigJam y Figma. No asumir que pueden abrir o editar esas herramientas sin una conexión verificada.
5. AG-004 y AG-005 implementarán la solución respetando la arquitectura de cinco capas y los contratos de API aprobados.
6. AG-006 verificará el cumplimiento de los requisitos, las restricciones de seguridad y los criterios de aceptación, y documentará la evidencia de las pruebas.
7. Ningún agente podrá modificar unilateralmente requisitos aprobados, introducir nuevos roles, alterar el modelo original de 21 tablas ni ejecutar operaciones críticas sin autorización humana.
8. No suponer integraciones automáticas entre OpenCode, Codex, Claude, ChatGPT, Figma o FigJam. Si no existe integración autorizada y comprobada, intercambiar resultados mediante archivos, enlaces o procedimientos manuales documentados.
9. La asignación de una herramienta a un agente indica una responsabilidad prevista; **no certifica que el agente esté instalado, conectado o ejecutándose**.

## 6. Agentes de IA para el desarrollo

| Código | Agente | Responsabilidad | Entregable | Restricción |
|---|---|---|---|---|
| AG-001 | Analista de requisitos | Analizar propuesta y DERCAS, detectar ambigüedades, mantener trazabilidad | Matriz de requisitos y criterios | No aprobar cambios unilateralmente |
| AG-002 | UML / FigJam | Definir actores, casos de uso, actividades, secuencias y flujos | Especificaciones y diagramas | No alterar requisitos aprobados |
| AG-003 | UI/UX / Figma | Diseñar wireframes, componentes y prototipos móvil/escritorio | Pantallas y enlaces de prototipos | No declarar prototipo como código funcional |
| AG-004 | Frontend | Implementar Ionic/Angular y consumir API autorizada | Código frontend y pruebas | No omitir validación del backend |
| AG-005 | Backend | Implementar API, servicios, seguridad, Sequelize y MySQL | Código backend, migraciones y pruebas | No ejecutar migraciones destructivas sin aprobación |
| AG-006 | QA | Verificar requisitos, integración, permisos, accesibilidad y regresión | Casos, resultados y evidencias | No marcar aprobado sin evidencia |
| AG-007 | Coordinador/orquestador | Crear tareas, resolver dependencias, asignar responsables y registrar decisiones | Tablero de tareas y revisiones | No sustituir la aprobación humana |

Los agentes pueden ser roles de trabajo configurados en una herramienta; **no equivalen automáticamente a siete procesos autónomos conectados**.

### 6.1. Marca institucional y logotipo oficial

**Referencia visual obligatoria:** `docs/marca/logo-licoreria-junin-currinchero.png` (archivo suministrado por el responsable del proyecto e incluido en este paquete). El logotipo presenta emblema circular azul y amarillo, botellas y jarra, cinta roja «LICORERÍA», nombre «JUNÍN» en azul y «CURRINCHERO» sobre banda azul. Conservar proporciones, composición, texto y legibilidad. No sustituir, deformar ni rediseñar el logo sin aprobación humana.

**Paleta institucional aprobada por el responsable:**

| Clasificación | Color | Código hexadecimal | Complementario indicado | Código hexadecimal |
|---|---|---|---|---|
| Primario | Rojo | `#C62828` | Cian oscuro | `#28C6C6` |
| Primario | Azul | `#1565C0` | Naranja | `#C07015` |
| Primario | Amarillo | `#F9A825` | Azul violeta | `#2576F9` |
| Secundario | Verde esmeralda | `#2E7D32` | Magenta | `#7D2E79` |
| Secundario | Naranja cálido | `#EF6C00` | Azul intenso | `#0083EF` |
| Secundario | Violeta | `#7B1FA2` | Verde lima | `#46A21F` |
| Terciario | Rojo anaranjado | `#D84315` | Azul turquesa | `#15AAD8` |
| Terciario | Verde azulado | `#00897B` | Rojo coral | `#89000E` |
| Terciario | Amarillo verdoso | `#9E9D24` | Violeta azulado | `#24259E` |

Los pares complementarios se registran **tal como los proporcionó el responsable**, sin afirmar que sean complementos cromáticos exactos.

**Aplicación de la marca por los agentes:**

1. **AG-003 (Figma/UI/UX):** usar el logo oficial y la paleta como base de prototipos. Priorizar azul `#1565C0` en navegación, rojo `#C62828` en acentos de marca y amarillo `#F9A825` en énfasis puntuales. Secundarios, terciarios y complementarios son opciones de apoyo; evitar usar todos simultáneamente.
2. **AG-004 (Frontend y AdminWeb):** centralizar colores en tokens CSS/SCSS o variables de tema y reutilizarlos en ambas interfaces. Integrar el logo desde los activos del proyecto y preservar su relación de aspecto. No aplicar colores arbitrarios sin revisión.
3. **AG-006 (pruebas):** comprobar contraste, legibilidad, estados de foco, botones y accesibilidad conforme al objetivo WCAG 2.2 AA. Si una combinación no alcanza el contraste necesario, proponer una variante de aplicación o un color de texto accesible sin modificar silenciosamente los códigos institucionales.
4. **AG-007 (coordinación):** contrastar cada cambio visual con el DERCAS, los diseños aprobados y este logo. Someter cambios de identidad visual a aprobación humana.
5. **Repositorios:** implementar marca en `Frontend` y `AdminWeb`; el `Backend` solo manejará referencias o datos de marca si un requisito lo justifica. Copiar el logo a las rutas de activos que realmente utilice cada proyecto; `docs/marca/` es la referencia documental propuesta.
6. **Control de versiones:** la tarea de marca debe estar terminada, revisada y **aprobada explícitamente** antes de hacer un commit en cada repositorio afectado, siguiendo la sección 11.2. No realizar commits automáticos durante el desarrollo.

**Conflictos de fuentes:** si la versión aprobada del DERCAS o de la propuesta contradice esta paleta, documentar la discrepancia y solicitar decisión humana antes de cambiar los diseños.

## 7. Orquestación obligatoria

### 7.1 Ciclo de trabajo

`Propuesta aprobada → DERCAS vigente → AG-007 asigna TSK-XXX → AG-001 verifica requisitos → AG-002 prepara UML/FigJam → AG-003 prepara Figma → AG-004 y AG-005 implementan según dependencias → AG-006 prueba → revisión humana → aprobación o REV-XXX → corrección y repetición`.

No se trata de una secuencia rígida: una incidencia puede devolver el trabajo a requisitos, UML, Figma, frontend o backend.

### 7.2 Contrato de tarea

Cada tarea deberá contener:

```yaml
id: TSK-001
requisito_origen: RF-XXX
objetivo: "Descripción verificable"
fuentes_aprobadas: ["documento y versión"]
agente_responsable: AG-XXX
dependencias: []
archivos_permitidos: []
acciones_prohibidas: []
criterios_aceptacion: []
entregables: []
evidencia: []
estado: pendiente
revision: pendiente
aprobacion_humana: pendiente
```

Estados posibles: `pendiente`, `listo`, `en ejecución`, `en revisión`, `observado`, `en corrección`, `bloqueado` y `aprobado`.

### 7.3 Ciclo de corrección

1. AG-007 comprueba fuentes, alcance, permisos y dependencias.
2. El agente responsable genera el entregable versionado.
3. AG-006 verifica requisitos y registra evidencia.
4. Si falla, abrir `REV-XXX`, explicar hallazgo, requisito afectado y responsable.
5. Corregir, incrementar versión y repetir pruebas afectadas.
6. La persona responsable aprueba formalmente los cambios de alcance y acciones críticas.
7. AG-007 actualiza trazabilidad y registra la decisión.
8. Solo después de finalizar y obtener aprobación humana explícita de la tarea, registrar el commit en el repositorio afectado, siguiendo la sección 11.2. No hacer `push` sin autorización.

## 8. Prohibiciones y límites de la aplicación

- No crear un tercer rol llamado Cliente.
- No permitir que el registro público cree cuentas Administrador.
- No revelar pedidos ni datos de otros usuarios.
- No permitir compras de alcohol sin las verificaciones legales y de edad aplicables.
- No confirmar transferencias por la sola carga de un comprobante; la validación es administrativa.
- No permitir que asistentes de IA aprueben pagos, modifiquen estados, registren compras o cambien inventario.
- No permitir acceso directo de AAC a MySQL ni exponer credenciales.
- No inventar precios, existencias, políticas ni estados de pedido.
- No implementar pasarelas bancarias automáticas, logística externa ni modo sin conexión sin aprobación expresa.
- No modificar el modelo de 21 tablas, las 21 vistas o los requisitos existentes sin solicitud de cambio aprobada.

## 9. Prohibiciones y límites de los agentes de desarrollo

- No borrar archivos, datos, tablas, ramas ni historiales sin autorización humana explícita.
- No modificar DERCAS, la propuesta, reglas de seguridad o sus propias instrucciones sin revisión.
- No desplegar en producción ni usar credenciales productivas en pruebas sin autorización.
- No guardar secretos, contraseñas, tokens o datos personales reales en prompts, commits o logs.
- No ejecutar comandos destructivos ni instalar dependencias nuevas sin explicar el impacto y obtener permiso según el entorno.
- No asumir acceso a servicios externos o archivos de Figma/FigJam sin comprobarlo.
- No declarar una tarea aprobada solo porque el código compile o una maqueta se vea bien.

## 10. Trazabilidad y criterios de aceptación

Conservar la cadena: `RF/RNF → CU (FigJam) → UI (Figma) → endpoint/servicio → código → caso de prueba → evidencia → aprobación`.

Verificar especialmente:
- RBAC: solo Administrador y Usuario; controles de permisos en backend.
- Pedidos: un usuario no puede consultar pedidos ajenos, incluido AAC-002.
- Inventario: no permitir existencias negativas y respetar stock mínimo.
- Pagos: transferencia pendiente hasta validación administrativa.
- Multiplataforma: flujos principales utilizables en Android y navegador de computadora.
- Seguridad IA: entradas maliciosas no modifican permisos ni instrucciones internas.
- Calidad: pruebas funcionales, integración, autorización y regresión antes de aprobar.

## 11. Control de cambios

Para cualquier cambio de alcance crear `CR-XXX` con motivo, requisitos afectados, impacto en FigJam/Figma/API/base de datos/código/pruebas, responsable y decisión humana. Mantener versiones y enlaces de evidencia. No sobrescribir silenciosamente entregables aprobados.

### 11.1 Repositorios oficiales de GitHub

El proyecto utiliza **tres repositorios Git independientes**. Estas son las URL proporcionadas por el responsable del proyecto; verificar acceso y permisos antes de clonar o enviar cambios.

| Repositorio | Responsabilidad | URL GitHub (remoto `origin`) |
|---|---|---|
| **Backend** | Node.js, Express, servicios, API REST, Sequelize, MySQL, autenticación y pruebas del servidor; AG-005 | `https://github.com/alezandezmejiaz-lgtm/Backend.git` |
| **Frontend** | Aplicación del usuario con Ionic, Angular, TypeScript y Capacitor; AG-004 | `https://github.com/alezandezmejiaz-lgtm/Frontend.git` |
| **AdminWeb** | Interfaz web del administrador y sus módulos; AG-004, con coordinación de AG-007 | `https://github.com/alezandezmejiaz-lgtm/AdminWeb.git` |

- **No tratar los tres repositorios como carpetas de un solo repositorio Git.** Cada uno tiene su propia rama, historial, commits, revisiones y remoto `origin`.
- AG-007 identifica antes de cada tarea cuál o cuáles repositorios se verán afectados. Si una tarea requiere cambios en más de uno, coordinar contratos de API y registrar **un commit independiente por repositorio**, siempre después de completar y aprobar la tarea correspondiente; asociar los commits al mismo `TSK-XXX`.
- AG-001, AG-002, AG-003, AG-006 y AG-007 colaboran con los tres repositorios según el alcance. Mantener las referencias a la propuesta y al **DERCAS aplicado** accesibles para todos, sin asumir que `docs/` existe en cada repositorio; comprobar rutas y versiones antes de trabajar.
- No crear repositorios adicionales ni cambiar estas URL sin autorización humana. No afirmar que los remotos están configurados hasta comprobar `git remote -v`.

### 11.2 Regla obligatoria: commit SOLO al finalizar y aprobar una tarea

**Regla principal:** los agentes **NO ejecutarán `git commit` durante el desarrollo, las revisiones ni las correcciones de una tarea**. El commit se realizará **únicamente después de que la tarea esté terminada, verificada y aprobada explícitamente por la persona responsable**. No basta con que un agente indique «terminado», que el código compile o que las pruebas pasen.

**Flujo de trabajo para cada `TSK-XXX`:**

1. **Asignación:** AG-007 identifica tarea, repositorio(s), RF/RNF y criterios de aceptación del DERCAS; comprueba rama y permisos.
2. **Desarrollo:** AG-001 a AG-005 realizan el trabajo correspondiente en la rama autorizada. Pueden editar y guardar archivos, pero **sin crear commits**.
3. **Pruebas:** AG-006 ejecuta las comprobaciones pertinentes, registra resultados reales y devuelve observaciones si corresponde.
4. **Correcciones:** el agente responsable corrige y AG-006 vuelve a revisar. Repetir tantas veces como sea necesario; **sin commits mientras la tarea esté pendiente, observada o en corrección**.
5. **Entrega para revisión:** AG-007 presenta al responsable humano resumen, archivos modificados, `git diff`, pruebas, requisitos relacionados y propuesta de mensaje de commit.
6. **Aprobación explícita:** esperar una confirmación inequívoca del responsable humano de que **la tarea está finalizada y aprobada y autoriza el commit**. Si no la hay, detenerse antes de `git add`/`git commit`.
7. **Commit posterior a la aprobación:** en el repositorio correcto, verificar `git status`, preparar **solo archivos aprobados** mediante `git add <rutas>` y ejecutar **un commit por tarea aprobada y por repositorio afectado**, con ID de tarea. Si después aparece una corrección, abrir nueva tarea o nueva aprobación y crear un commit posterior; no reescribir el anterior.
8. **Registro y GitHub:** AG-007 registra hash, repositorio, rama, `TSK-XXX`, RF/RNF, pruebas y aprobación. **`git push`, pull request y merge requieren autorización específica**, salvo que el responsable haya establecido previamente una política explícita para esas acciones. Nunca usar `force push` sin permiso.

**Estados que impiden commit:** `pendiente`, `en ejecución`, `en revisión`, `observado`, `en corrección`, `bloqueado`, `pruebas pendientes`, `aprobación pendiente`.

**Estado que habilita commit:** `finalizada y aprobada por humano`, con autorización de commit registrada. **AG-007 coordina y verifica, pero no reemplaza la aprobación humana.**

**Formato de commit:** `tipo(área): descripción breve [TSK-XXX]`, usando `feat`, `fix`, `docs`, `test`, `refactor` o `chore` según corresponda.

Ejemplo **solo después de la aprobación**, ejecutado dentro del repositorio Backend (no en los otros):

```bash
git remote -v
git status
git diff
git add src/routes/pedidos.js src/services/pedidos.service.js
git commit -m "feat(pedidos): implementar consulta autorizada [TSK-014]"
# git push -u origin feature/TSK-014-pedidos  # Solo con autorización de envío
```

Las rutas y nombres del ejemplo son ilustrativos: comprobar los archivos existentes antes de usarlos. **No ejecutar `git add .` indiscriminadamente**, ni incluir `.env`, credenciales, tokens, información personal o archivos temporales. Si la tarea afecta Frontend o AdminWeb, ejecutar los comandos **dentro de ese repositorio**, nunca desde Backend.

**Responsabilidades:** AG-001 vincula RF/RNF y DERCAS; AG-002/003 mantienen diagramas y diseños versionados cuando proceda; AG-004/005 implementan; AG-006 verifica; AG-007 coordina la aprobación y documenta los commits de los repositorios correspondientes. GitHub permite revisión y respaldo remoto, pero no sustituye la revisión humana.

## 12. Primera tarea sugerida

**TSK-001 — Auditoría documental inicial:** AG-007 solicita a AG-001 comparar la propuesta y DERCAS vigentes; identificar campos pendientes, inconsistencias, decisiones sin aprobar y cobertura de los 21 módulos/vistas, 21 tablas, RF-001–RF-255 y RNF-001–RNF-072. AG-001 entrega matriz de hallazgos; AG-006 revisa; una persona aprueba las correcciones antes de iniciar UML o programación.

---

**Nota académica:** En este proyecto, DERCAS se utiliza como documento de especificación de requerimientos y criterios de aceptación, ampliado con coordinación multiagente. No presentar esta adaptación como una metodología universal estandarizada sin una fuente que lo respalde.

## 13. Uso de los perfiles entregados

- OpenCode: consultar `.opencode/agents/ag-001.md` a `ag-007.md`; son definiciones propuestas de subagentes. Revisar la versión instalada y los permisos efectivos antes de habilitar escritura o ejecución.
- Codex: `codex/perfiles/` contiene instrucciones de rol que se pueden invocar en sesiones separadas; `AGENTS.md` es la instrucción común del repositorio. No asumir que siete perfiles equivalen a siete agentes paralelos configurados.
- Registrar cada cambio lógico aprobado en un commit Git independiente. No crear commits automáticamente: presentar cambios y evidencia, solicitar aprobación humana antes del commit y autorización correspondiente antes de push/merge, según la sección 11.2.
- Separar los entregables de análisis (`docs/`), diseño (Figma/FigJam), frontend y backend. Los repositorios oficiales son Backend, Frontend y AdminWeb, definidos en la sección 11.1.

## 14. Las doce mejoras DERCAS como controles de trabajo

1. RBAC validado en backend.
2. Orquestación por AG-007 con aprobación humana.
3. Contexto compartido solo de fuentes versionadas y aprobadas.
4. Validación automática de requisitos cuando exista implementación.
5. Trazabilidad RF/RNF → UML → Figma → código → pruebas.
6. CI/CD propuesto, no declarar activo sin pipeline ejecutado.
7. Seguridad y gobernanza de agentes, mínimos privilegios y protección de secretos.
8. Versionado con Git y GitHub, un commit por cambio lógico aprobado, solicitudes de cambio y plan de reversión.
9. Métricas de calidad y evaluación con resultados medidos.
10. RAG opcional, sujeto a necesidad y autorización; no es dependencia obligatoria.
11. Accesibilidad web WCAG 2.2 AA como objetivo verificable.
12. Monitoreo y mejora continua con incidentes y evidencias.

## 15. Estado de implementación

**Documentado:** roles, límites, diagramas y perfiles propuestos. **Pendiente de verificar:** instalación de herramientas, enlaces Figma/FigJam, proveedores IA, ejecución de pruebas, integración CI/CD, despliegue y aprobaciones. No reportar como realizado lo que solo esté especificado.


## 16. Inventario de fuentes sincronizadas (paquete de referencia)

| Ruta relativa desde `AGENTS.md` | Contenido y uso |
|---|---|
| `docs/Propuesta_y_DERCAS_Licoreria_Junin_Currinchero_Completado.pdf` | Documento integrado: propuesta y DERCAS; fuente principal de RF, RNF y criterios de aceptación |
| `docs/diagramas/arquitectura-por-capas.png` | Arquitectura original de cinco capas y tecnologías |
| `docs/diagramas/arquitectura-con-ia.png` | Ampliación con asistentes AAC-001, AAC-002 y AAC-003 |
| `docs/diagramas/modelo-entidad-relacion.png` | Diagrama entidad-relación original de 21 tablas |
| `docs/marca/logo-licoreria-junin-currinchero.png` | Logotipo institucional suministrado |

**Instrucción de lectura para OpenCode y Codex:** antes de iniciar `TSK-XXX`, abrir este `AGENTS.md`, verificar la existencia de las rutas anteriores, leer el documento rector (propuesta y después DERCAS), consultar los diagramas pertinentes y registrar los RF/RNF y criterios aplicables. Si el entorno no puede leer el PDF o las imágenes, pedir una extracción o revisión humana; nunca afirmar haberlos consultado sin hacerlo.

**Despliegue en repositorios:** `Backend`, `Frontend` y `AdminWeb` son repositorios independientes. Este paquete es una plantilla documental para instalar en cada repositorio o en un espacio de trabajo compartido con rutas comprobadas. La distribución de archivos no equivale a `git add`, `git commit`, `git push` ni a aprobación. No ejecutar esas operaciones sin la autorización prevista en la sección 11.2.
