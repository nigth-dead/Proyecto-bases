# 🏆 Proyecto Integrador: Administración de Bases de Datos

**Valor Total:** 40 Puntos  
**Modalidad:** Equipos 5 integrantes  
**Entorno:** SQL Server 2022 (Docker / Local) + Control de Versiones en Git (GitHub / GitLab)  
**Base de Datos:** `AdventureWorks2014`

---

## 🎯 Objetivo General
Implementar, asegurar y optimizar un modelo de base de datos empresarial (`AdventureWorks2014`) mediante una adecuada gestión de recursos, seguridad granular por esquemas, programación transaccional en T-SQL y estrategias de respaldo y recuperación ante desastres, documentando y versionando todo el ciclo de administración en un repositorio profesional de **Git**.

---

## 📂 Estructura Obligatoria del Repositorio Git

Cada equipo deberá crear un repositorio en GitHub/GitLab con la siguiente estructura exacta de carpetas y archivos. **No se aceptarán entregas por correo ni archivos sueltos.**

```text
proyecto-integrador-abd/
│
├── README.md                          # Guía rápida de despliegue, integrantes y enlace al .ZIP
│
├── 01_restauracion/                   # Fase 1: Restauración y limpieza base (3 pts)
│   ├── AdventureWorks2014.bak         # Archivo de respaldo base (o enlace si excede 100 MB)
│   ├── adventureworks2008_schema.gif  # Archivo que contiene los schemas y distribución de tablas
│   ├── 01_restore_adventureworks.sql  # Script de restauración completa de AdventureWorks2014
│   └── 02_limpieza_objetos.sql        # Script dinámico de eliminación de SPs predeterminados
│
├── 02_seguridad_usuarios/             # Fase 2: Seguridad y control de acceso (7 pts)
│   └── 01_logins_y_roles.sql          # Creación de Logins, Users, Roles y asignación de permisos
│
├── 03_programacion_tsql/              # Fase 3 y 4: UDFs, Vistas y SPs (20 pts)
│   ├── 01_funciones_escalares.sql     # UDFs (Edad, IVA 16%, Crédito aprobado)
│   ├── 02_vistas.sql                  # Vistas consolidadas (Empleados, Personas, Clientes)
│   ├── 03_spi_employee.sql            # SPs (Insert) - Empleados
│   ├── 04_spu_employee.sql            # SPs (Update) - Empleados
│   ├── 05_spd_employee.sql            # SPs (Delete) - Empleados
│   ├── 06_sps_employee.sql            # SPs (Select) - Empleados
│   ├── 07_spi_product.sql             # SPs (Insert) - Productos
│   ├── 08_spu_product.sql             # SPs (Update) - Productos
│   ├── 09_spd_product.sql             # SPs (Delete) - Productos
│   ├── 10_sps_product.sql             # SPs (Select) - Productos
│   ├── 11_spi_customer.sql            # SPs (Insert) - Customers
│   ├── 12_spu_customer.sql            # SPs (Update) - Customers
│   ├── 13_spd_customer.sql            # SPs (Delete) - Customers
│   └── 14_sps_customer.sql            # SPs (Select) - Customers
│   
├── 04_respaldos_recuperacion/         # Fase 5: Continuidad del negocio (4 pts)
│   └── 01_rutina_respaldos.sql        # Scripts de Backup Full, Diferencial y Log (.bak / .trn)
│ 
├── 05_notebooks/                      # Ejecución interactiva en VS Code (MSSQL) con salidas visibles
│   ├── 01_test_transactions.ipynb     # Pruebas unitarias de cada  demostrando estados 200, 400 y 500 de cada Sp
│   ├── 02_test_selects.ipynb          # Pruebas unitarias 
│   ├── 03_simulacro_restauracion.ipynb  # Script de recuperación Point-in-Time (STOPAT)
│   └── 04_pruebas_permisos.ipynb        # Scripts de validación (GRANT/DENY) por área funcional
│
└── 06_entrega_final/                  # Fase 6: Cierre y documentación ejecutiva (6 pts)
    └── reporte-final.pdf              # Documento integrador oficial del equipo
```

---

## 📊 Matriz de Evaluación y Puntajes

| Módulo / Fase | Carpeta en Repositorio | Entregables y Criterios Principales | Puntaje |
| :--- | :--- | :--- | :---: |
| **1. Restauración y Limpieza** | `01_restauracion/` | Archivo `AdventureWorks2014.bak`, script de restauración y script dinámico de limpieza de SPs predeterminados. | **3 pts** |
| **2. Seguridad y Usuarios** | `02_seguridad_usuarios/` | Administrador (`db_owner`), usuarios por área funcional con permisos granulares (`GRANT`/`DENY`), contraseñas ≥ 12 caracteres y usuario `db_backupoperator`. | **7 pts** |
| **3. Programación Avanzada T-SQL** | `03_programacion_tsql/` | 3 Funciones Escalares (UDFs) + 12 Stored Procedures CRUD (`Employee`, `Product`, `Customer`) con manejo de transacciones (`TRY/CATCH`) y estados (`200/400/500`). | **14 pts** |
| **4. Vistas Corporativas** | `03_programacion_tsql/` | 3 Vistas consolidadas optimizadas (`vw_EmpleadosDepartamento`, `vw_DirectorioPersonasFinanzas`, `vw_ClientesTerritorios`) sin `SELECT *`. | **6 pts** |
| **5. Respaldos y Recuperación** | `04_respaldos_recuperacion/` | Modelo `FULL`, rutinas de respaldo (`.bak` y `.trn`) con `db_backupoperator` y demostración en vivo de recuperación `STOPAT`. | **4 pts** |
| **6. Documento Integrador** | `05_entrega_final/` | Reporte ejecutivo en PDF (`reporte-final.pdf`) con arquitectura de seguridad, documentación técnica, evidencias y defensa en vivo. | **6 pts** |
| **TOTAL** | **Repositorio Completo** | **Código versionado en Git, respaldo `.ZIP`, reporte PDF y defensa presencial.** | **40 pts** |

---

## 📋 Requerimientos Técnicos Detallados

### 1. Restauración y Limpieza de la Base de Datos (3 Puntos)
* **Archivo Base:** Incluir `AdventureWorks2014.bak` dentro de la carpeta `01_restauracion/` *(Nota: Si GitHub bloquea la subida por pesar más de 100 MB, utilizar Git LFS o incluir el enlace directo en `01_restauracion/README.md`)*.
* **Restauración (`01_restore_adventureworks.sql`):** Restaurar completamente la base de datos `AdventureWorks2014` en su instancia de SQL Server.
* **Limpieza (`02_limpieza_objetos.sql`):** Programar un script dinámico (usando cursores o `sys.procedures`) que elimine **todos** los procedimientos almacenados predeterminados una vez finalizada la restauración, dejando la base limpia para su arquitectura.

### 2. Seguridad, Esquemas y Administración de Usuarios (7 Puntos)
* **Administrador:** Crear un usuario administrador (`db_owner`) con control total sobre la base de datos.
* **Usuarios por Área Funcional:** Crear logins y usuarios específicos con permisos estrictos de lectura y escritura (`SELECT`, `INSERT`, `UPDATE`, `DELETE`) limitados únicamente a los esquemas de cada área funcional (`HumanResources`, `Production`, `Sales`), aplicando ocultamiento de metadatos (`DENY VIEW DEFINITION`) para áreas ajenas.
* **Política de Contraseñas:** Todas las cuentas deben contar con contraseñas robustas de **mínimo 12 caracteres** que incluyan mayúsculas, minúsculas y números.
* **Operador de Respaldos:** Crear un usuario exclusivo asignado al rol `db_backupoperator` sin permisos de lectura/escritura sobre las tablas de negocio.

### 3. Programación Avanzada T-SQL: Funciones y SPs (14 Puntos)
* **Funciones Escalares (UDFs):**
  1. `dbo.fn_CalcularEdad`: Calcula la edad exacta en años a partir de `BirthDate`.
  2. `dbo.fn_CalcularPrecioConIVA`: Aplica el 16% de IVA al precio de lista (`ListPrice`).
  3. `dbo.fn_EvaluarCredito`: Retorna `'Aprobado'` o `'No aprobado'` evaluando si el límite de crédito es mayor o igual a `$7,500`.
* **Procedimientos Almacenados CRUD (`spi_`, `spu_`, `spd_`, `sps_`):**
  Desarrollar el ciclo completo (Insertar, Actualizar, Eliminar y Consultar) para las entidades:
  * `Employee` (Esquema `HumanResources`)
  * `Product` (Esquema `Production`)
  * `Customer` (Esquema `Sales`)
* **Estándares Obligatorios en todos los SPs:**
  * **Consultas (`sps_`):** Deben permitir obtener **uno o todos los registros** dentro del mismo procedimiento mediante parámetros opcionales (`ISNULL`).
  * **Protocolo de Respuesta (`OUTPUT`):** Retornar `@Estado` (`200` Éxito, `400` Validación/Duplicado/Faltante, `500` Error interno) y `@Mensaje` descriptivo.
  * **Retorno de Identificador:** Generar y retornar el `ID` del nuevo registro insertado mediante variable `OUTPUT`.
  * **Control Transaccional:** Uso estricto de bloques `TRY...CATCH`, `BEGIN TRANSACTION`, `COMMIT` y `ROLLBACK` con `ERROR_MESSAGE()`.
  * **Integración en Consultas:** Las consultas deben invocar las funciones escalares creadas para devolver:
    * *Empleados:* `Id`, `FirstName`, `MiddleName`, `JobTitle`, `BirthDate`, `MaritalStatus`, `Gender` + **Edad calculada**.
    * *Productos:* `Id`, `Name`, `ProductNumber` + **Precio con IVA (16%)**.
    * *Clientes:* `Id`, `FirstName`, `MiddleName`, `AccountNumber`, `CreditLimit` + **Estatus de crédito**.

### 4. Vistas Corporativas Consolidadas (6 Puntos)
Crear 3 vistas optimizadas (evitando `SELECT *` y usando nombres calificados `Esquema.Tabla`):
1. `vw_EmpleadosDepartamento`: Información básica de los empleados junto con su departamento y turno correspondiente.
2. `vw_DirectorioPersonasFinanzas`: Personas con su correo electrónico, número de teléfono, tipo de teléfono e información de tarjeta de crédito asociada.
3. `vw_ClientesTerritorios`: Clientes (`Customers`) vinculados con sus respectivos territorios y regiones asignadas.

### 5. Estrategia de Respaldos y Recuperación ante Desastres (4 Puntos)
* **Modelo de Recuperación:** Configurar `AdventureWorks2014` en modo `FULL` y ejecutar mediante el usuario `db_backupoperator` una rutina automatizada o programada que genere un **Respaldo Completo (`.bak`)** y una secuencia de **Respaldos Transaccionales (`.trn`)** con marca de tiempo.
* **Simulacro en Vivo:** Durante la presentación final, ejecutar una modificación o borrado accidental mediante sus Stored Procedures y demostrar en vivo la restauración secuencial (`NORECOVERY` -> `RECOVERY` / `STOPAT`) recuperando la integridad de los datos.

---

## 📄 6. Documento Integrador (`05_entrega_final/reporte-final.pdf`) (6 Puntos)

Cada equipo deberá incluir obligatoriamente en `05_entrega_final/reporte-final.pdf` el **documento integrador oficial del equipo**, elaborado con calidad profesional y estructurado con los siguientes apartados:

1. **Portada Institucional:**
   * Logotipos oficiales de la **Universidad Veracruzana** y de la **Facultad de Estadística e Informática (FEI)**.
   * Nombre de la experiencia educativa: **Administración de Bases de Datos**.
   * Título del proyecto: **Administración, Seguridad y Optimización de la Base de Datos Empresarial AdventureWorks2014**.
   * Integrantes del equipo con sus respectivos roles operativos (ej. *DBA Líder / Arquitectura*, *Especialista en Seguridad y Roles*, *Ingeniero de Programación T-SQL y Respaldos*).
   * Fecha de entrega y nombre del docente.

2. **Introducción y Justificación:**
   * Contexto operativo de la administración de bases de datos empresariales y riesgos asociados a la falta de control de acceso, consultas no optimizadas y ausencia de planes de recuperación ante desastres.
   * Objetivos general y específicos de la implementación técnica realizada.

3. **Arquitectura de Seguridad y Control de Acceso (Resumen Técnico):**
   * Matriz de permisos y roles: Tabla detallada especificando los Logins, Users, Roles personalizados, esquemas autorizados (`HumanResources`, `Production`, `Sales`), restricciones de visibilidad (`DENY VIEW DEFINITION`) y privilegios del operador de respaldos (`db_backupoperator`).
   * Diagrama o explicación de la segregación de funciones (Principio de Privilegio Mínimo).

4. **Implementación de Programación T-SQL y Vistas (Lógica de Negocio):**
   * Explicación técnica del diseño de las 3 funciones escalares (`UDFs`) y las 3 vistas corporativas consolidadas (`WITH SCHEMABINDING` / optimización de `JOIN`s).
   * Arquitectura transaccional de los 12 procedimientos almacenados (`spi_`, `spu_`, `spd_`, `spr_`), detallando el flujo de validación previa, bloques `TRY...CATCH`, control `COMMIT/ROLLBACK` y estandarización de códigos de respuesta (`200`, `400`, `500`).

5. **Estrategia de Continuidad del Negocio (Respaldos y Recuperación):**
   * Política de periodicidad definida (Full, Diferencial y Transaction Logs) y configuración del modelo de recuperación `FULL`.
   * Documentación técnica del procedimiento de recuperación en el tiempo (`STOPAT`) aplicado durante el simulacro de incidente.

6. **Evidencias de Ejecución (Capturas Clave):**
   * Capturas claras y legibles del contenedor de **Docker** ejecutando SQL Server y los volúmenes de respaldo mapeados.
   * Ejecución de scripts y pruebas unitarias desde **VS Code / DBeaver** mostrando los outputs de estados `200`, `400` y `500`.
   * Pruebas de aislamiento de metadatos (captura del explorador de objetos conectado con un usuario de área mostrando la ceguera lógica de los demás esquemas).
   * Evidencia de la generación física de archivos `.bak` / `.trn` y la restauración exitosa tras el borrado simulado.
   * Rol de los integrantes que hicieron del proyecto
   * Conclusiones individuales y una general sobre el proceso de administración de una base de datos

---

## 📅 Cronograma de Revisiones y Entrega Final

| Hito / Revisión | Alcance Evaluado en Repositorio Git | Formato |
| :--- | :--- | :--- |
| **Revisión de Avance 1** | Carpetas `01_restauracion` (`AdventureWorks2014.bak`, restore y limpieza) y `02_seguridad_usuarios`. | Commit en Git + Revisión en Aula |
| **Revisión de Avance 2** | Carpeta `03_programacion_tsql` (Funciones, Vistas y SPs con manejo de estados 200/400/500). | Commit en Git + Revisión en Aula |
| **Entrega y Defensa Final** | Repositorio completo al 100%, `05_entrega_final/reporte-final.pdf`, enlace al respaldo `.ZIP` final en el `README.md` y demostración en vivo (máx. 20 min por equipo). | Commit Final + Presentación |

---

## 📝 Requisitos del `README.md` Principal
El archivo `README.md` en la raíz del repositorio funcionará como guía rápida de despliegue y deberá incluir:
1. Nombres completos, matrículas y roles de los integrantes del equipo.
2. Guía paso a paso del orden de ejecución de los scripts para levantar el entorno desde cero.
3. Enlace de descarga directa (Google Drive / OneDrive con permisos abiertos) al archivo **`.ZIP`** que contiene el respaldo completo (`.bak`) final de la base de datos configurada y lista para producción.

---

## 🚀 Uso de esta plantilla

Esta plantilla contiene tareas pendientes, no una solución terminada. Completen los scripts y ejecuten las pruebas; las celdas de los notebooks no contienen resultados precargados.

### Datos del equipo

| Nombre completo | Matrícula | Rol operativo |
| --- | --- | --- |
| PENDIENTE | PENDIENTE | PENDIENTE |
| PENDIENTE | PENDIENTE | PENDIENTE |
| PENDIENTE (opcional) | PENDIENTE | PENDIENTE |

**Docente:** PENDIENTE  
**Fecha de entrega:** PENDIENTE  
**Enlace público de descarga del ZIP final:** PENDIENTE

### Inicio desde cero

1. Creen su repositorio a partir de esta plantilla (Use this template en GitHub, si está habilitado) y clonen **el repositorio de su equipo**. En GitLab pueden importar/copiar la plantilla a su propio proyecto.
2. Dispongan de SQL Server 2022, local o en Docker, y de un cliente SQL. Registren versión, servidor, puerto y rutas de datos/respaldos en su documentación, sin publicar credenciales. Si usan Docker, documenten el contenedor y los volúmenes persistentes que configuraron.
3. Sigan `01_restauracion/README.md` para obtener el respaldo y el diagrama. Las rutas usadas por RESTORE y BACKUP corresponden al servidor SQL o al interior del contenedor, no necesariamente a su equipo cliente.
4. Completen y ejecuten `01_restauracion/01_restore_adventureworks.sql`; después, revisen y ejecuten `02_limpieza_objetos.sql` sobre la base de laboratorio recién restaurada.
5. Completen y ejecuten `02_seguridad_usuarios/01_logins_y_roles.sql`. Usen secretos locales; no incluyan contraseñas reales en Git ni en las salidas de los notebooks.
6. Completen y ejecuten los scripts de `03_programacion_tsql/` en orden numérico: funciones, vistas y los doce procedimientos. Documenten y apliquen antes cualquier cambio de modelo que sus objetos requieran.
7. Completen `04_respaldos_recuperacion/01_rutina_respaldos.sql`, verifiquen permisos y rutas, y generen la cadena de respaldos.
8. Ejecuten los cuatro notebooks de `05_notebooks/`, seleccionando un entorno compatible con celdas SQL y su conexión. Si su editor no ejecuta ese kernel, ejecuten el SQL en su cliente y documenten las evidencias y resultados reales en las celdas Markdown. Guarden las salidas y eliminen secretos antes de hacer commit.
9. Elaboren `06_entrega_final/reporte-final.pdf`, suban el ZIP final a un servicio de archivos y reemplacen el campo de enlace anterior. Comprueben su acceso sin iniciar sesión.
10. Revisen los cambios con `git diff`, creen commits por avance y publiquen en el remoto de su equipo con `git push`.

### Aclaraciones de la plantilla

- Se conserva íntegro el enunciado anterior. Para resolver su discrepancia de numeración, esta plantilla sigue el árbol obligatorio: notebooks en `05_notebooks/` y reporte en **`06_entrega_final/reporte-final.pdf`**. Las referencias del enunciado a `05_entrega_final/` deben confirmarse con el docente.
- Se usa el prefijo **`sps_`** para consultas, conforme al árbol y los requisitos técnicos; el apartado del documento también menciona `spr_`.
- Verifiquen el modelo restaurado: `Sales.Customer` de AdventureWorks2014 no incluye `CreditLimit`. Antes de implementar crédito, acuerden con el docente una extensión o fuente de datos, documenten la decisión y agreguen su migración versionada. No asuman que todos los clientes tienen una persona asociada.
- `HumanResources.Employee.BusinessEntityID` se relaciona con `Person.BusinessEntity` y `Person.Person`; definan qué dependencias crea cada operación. No asuman que el identificador de empleado se genera directamente en Employee.
- El respaldo `.bak`, el diagrama `.gif` y el reporte `.pdf` se incorporan cuando existan archivos reales. No se incluyen archivos vacíos con esas extensiones. Las carpetas correspondientes contienen instrucciones para completarlos.
- Esta plantilla ignora respaldos, archivos de datos y ZIP para evitar subir archivos pesados o sensibles. Publiquen sus enlaces; si eligen Git LFS, configuren las reglas y retiren las exclusiones correspondientes antes de añadir archivos.

### Lista de entrega del equipo

- [ ] Integrantes, matrículas, roles y guía del entorno actualizados.
- [ ] Respaldo base y diagrama disponibles, con fuente y acceso comprobados.
- [ ] Restauración y limpieza revisadas en una base de laboratorio.
- [ ] Roles y permisos verificados con conexiones de cada usuario.
- [ ] Tres UDFs, tres vistas y doce SPs implementados.
- [ ] Pruebas por SP: parámetros, resultado esperado, resultado observado y estados aplicables 200/400/500; consultas de uno/todos y ausencia de registros.
- [ ] Evidencia de rollback y ausencia de transacciones abiertas tras errores.
- [ ] Cadena Full/diferencial/log y recuperación STOPAT demostradas.
- [ ] Notebooks ejecutados con evidencias legibles y sin secretos.
- [ ] PDF final en `06_entrega_final/` y enlace público del ZIP registrados.
