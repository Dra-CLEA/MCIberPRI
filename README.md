# Cyber Crisis Training Suite – README



> Tres simuladores de **gestión de crisis de ciberseguridad** para aula, ejecutados íntegramente en el navegador y diseñados para trabajar las dimensiones **técnica**, **legal** y de **comunicación**:
> 
> -   **DDoS RESPONSE: UCM COMMANDER** – defensa de portal de matrícula ante un ataque DDoS universitario.
>     
> -   **CRISIS PROTOCOL: WAR ROOM** – simulador de reputación corporativa y comité de crisis multi-caso.
>     
> -   **DATA LEAK RESPONSE: CISO CENTER** – respuesta a fuga de datos personales bajo RGPD/GDPR.
>     

---

## Índice General

1.  DDoS RESPONSE: UCM COMMANDER  
    1.1 Descripción y objetivo (ES)  
    1.2 Qué hace el código (ES)  
    1.3 Uso en el aula (ES)  
    1.4 Resolución orientativa (ES)  
    1.5 Overview (EN)  
    1.6 Class usage & walkthrough (EN)
    
2.  CRISIS PROTOCOL: WAR ROOM  
    2.1 Descripción y objetivo (ES)  
    2.2 Qué hace el código (ES)  
    2.3 Uso en el aula (ES)  
    2.4 Resolución orientativa (ES)  
    2.5 Overview (EN)  
    2.6 Class usage & walkthrough (EN)
    
3.  DATA LEAK RESPONSE: CISO CENTER  
    3.1 Descripción y objetivo (ES)  
    3.2 Qué hace el código (ES)  
    3.3 Uso en el aula (ES)  
    3.4 Resolución orientativa (ES)  
    3.5 Overview (EN)  
    3.6 Class usage & walkthrough (EN)
    
4.  Licencia
    
5.  Glosario de términos
    

---

## 1\. DDoS RESPONSE: UCM COMMANDER

### 1.1 Descripción y objetivo (ES)

> **Objetivo didáctico principal:** poner al alumnado en el rol de **equipo de crisis** de la **UCM**, gestionando un ataque **DDoS** durante el periodo de matrícula, equilibrando **SLA**, **satisfacción pública** y **presupuesto** mientras se documenta el incidente en un informe forense en **PDF/LaTeX**.

El simulador reproduce, en clave de **Command Center**, un incidente realista:

-   El portal de matrícula de la universidad sufre degradaciones y caídas.
    
-   El panel superior muestra tres **KPI**:
    
    -   **SLA WEB** (disponibilidad del portal).
        
    -   **SATISFACCIÓN** (percepción pública, afectada por redes sociales).
        
    -   **PRESUPUESTO** disponible para contramedidas.
        
-   Un **temporizador** cuenta 40 minutos de simulación: cada decisión tiene impacto temporal.
    

El alumnado debe:

1.  Constituir un **comité de crisis** con perfiles de **SSII**, Rectorado, **RedIRIS** y comunicación. 
    
2.  Diagnosticar si el problema es solo pico de matrícula o un ataque **DDoS**.
    
3.  Elegir medidas técnicas (**WAF**, **Scrubbing Center**, **Blackhole**) con impacto en tráfico, coste y reputación.
    
4.  Gestionar la comunicación con estudiantes y medios.
    
5.  Cerrar el incidente generando un informe forense y un informe en **LaTeX** listo para auditoría.
    

---

### 1.2 Qué hace el código (ES)

El simulador está implementado como **Single Page Application (SPA)** en **HTML**, **CSS** y **JavaScript**, sin backend: todo el modelo de estado vive en el navegador.

Elementos clave:

-   **Layout tipo dashboard**:
    
    -   Barra superior con marca `DDoS::UCM_COMMANDER`, **KPI** y temporizador.
        
    -   Panel izquierdo dinámico para contexto UCM y selección de roles.
        
    -   Panel central con indicador de **fase** (Acto 0–4), **Canvas** de topología y gráfico de tráfico en tiempo real con **Chart.js**.
        
    -   Panel derecho con **live logs (SIEM)** que reflejan saturación, errores **HTTP 503**, y ruido en redes sociales (`#UCMCaida`).
    
        
-   **Motor de simulación de tráfico**:
    
    -   Variables internas de tráfico normal, malicioso y mitigado.
        
    -   En cada tick de simulación se recalcula la carga total, se ajusta el **SLA** y se generan logs y mensajes (por ejemplo, **trending topic** en redes).
        
-   **Fases del ejercicio** (Actos):
    
    -   **Acto 0 – Comité de Crisis**: selección de perfiles (Resp. Comunicaciones, Jefe de Gestión Académica, Enlace **RedIRIS**, Gabinete de Comunicación, etc.), cada uno con coste y capacidades técnicas/comunicativas.
        
    -   **Acto 1 – Diagnóstico**: visualización de topología y curvas de tráfico para diferenciar carga legítima vs ataque volumétrico.
        
    -   **Acto 2 – Mitigación**: aplicación de medidas (perfiles de **WAF**, activación de **Scrubbing Center** de **RedIRIS**, uso de **Blackhole routing**).
        
    -   **Acto 3 – Comunicación**: decisiones de mensajes hacia estudiantes, medios y Rectorado.
        
    -   **Acto 4 – Cierre**: generación de informe forense en **PDF** y plantilla **LaTeX** con cronología, resumen ejecutivo y balance económico, mediante **jsPDF**, **JSZip** y **FileSaver**.
        
-   **Persistencia ligera**: el estado se mantiene en memoria durante la sesión; se puede reiniciar el escenario desde la barra superior.
    

---

### 1.3 Uso en el aula (ES)

Propuesta de secuencia:

1.  **Briefing inicial (5–10 min)**
    
    -   Explicar el contexto: ataque **DDoS** a un portal de matrícula universitario, impacto en **SLA** y reputación.
        
    -   Revisar los roles disponibles en el **comité de crisis** (técnicos, enlace con **ISP/RedIRIS**, comunicación, autoridad académica).
        
2.  **Acto 0 – Selección de equipo**
    
    -   En grupo, los estudiantes eligen el equipo con un presupuesto limitado de créditos.
        
    -   El docente puede pedir que justifiquen por qué priorizan, por ejemplo, a Enlace **RedIRIS** frente a otro perfil.
        
3.  **Acto 1 – Diagnóstico**
    
    -   Analizar con el grupo la curva de tráfico en el gráfico de **Chart.js**:
        
        -   Diferenciar crecimiento razonable por alta demanda vs pico incompatible con uso normal.
            
    -   Leer los logs de la consola **SIEM** para identificar errores **HTTP 503** y saturación de enlaces.
        
4.  **Acto 2 – Mitigación**
    
    -   Simular varias decisiones:
        
        -   Solo **WAF**.
            
        -   **WAF** + **Scrubbing Center**.
            
        -   Uso prematuro de **Blackhole**, discutiendo efectos sobre usuarios legítimos.
            
    -   Observar en tiempo real cómo cambian **SLA** y satisfacción.
        
5.  **Acto 3 – Comunicación**
    
    -   Trabajar mensajes hacia estudiantes: aviso en web, redes sociales, notas oficiales.
        
    -   Debatir riesgos de minimizar el incidente vs comunicar con transparencia.
        
6.  **Acto 4 – Informe forense**
    
    -   Generar el **PDF** y la versión **LaTeX**.
        
    -   Pedir al alumnado que identifique en el informe:
        
        -   Cronología clave.
            
        -   Decisiones técnicas tomadas.
            
        -   Impacto económico y reputacional.
            

---

### 1.4 Resolución orientativa (ES)

No hay una “única” solución correcta, pero sí una estrategia sólida que el docente puede usar como referencia:

1.  **Equipo de crisis equilibrado**
    
    -   Incluir al menos:
        
        -   Un perfil técnico de red (Resp. Comunicaciones/SSII).
            
        -   El enlace **RedIRIS**.
            
        -   El Gabinete de Comunicación.
            
        -   Una autoridad (Vicerrector TIC).
            

            
2.  **Diagnóstico adecuado**
    
    -   Reconocer, a partir del gráfico y logs, que el patrón es compatible con **DDoS** volumétrico: crecimiento agresivo, picos sostenidos, errores **HTTP 503**.
        
3.  **Mitigación escalonada**
    
    -   Ajustar primero el **WAF** y descartar causas internas (errores de código, mantenimiento).
        
    -   Activar **Scrubbing Center** de **RedIRIS** cuando el ataque supera la capacidad local.
        
    -   Reservar **Blackhole** como último recurso para preservar el resto de la infraestructura cuando la matrícula ya ha sido aplazada o reprogramada.
        
4.  **Comunicación proactiva**
    
    -   Mensajes oficiales claros indicando:
        
        -   Que se trata de un ataque de saturación, no de fuga de datos.
            
        -   Medidas tomadas y previsión de restablecimiento.
            
    -   Coordinación con canales institucionales (web, notas de prensa, redes).
        
5.  **Cierre e informe**
    
    -   El informe final debería reflejar un **SLA** razonable (no necesariamente 100 %), una **reputación** aceptable y un uso eficiente del presupuesto, justificando costes de mitigación vs impacto evitado.
        

---

### 1.5 Overview (EN)

**DDoS RESPONSE: UCM COMMANDER** is a browser-based **Command Center** simulation where students act as a university crisis team facing a large-scale **DDoS** attack during the enrolment period.

Key aspects:

-   Real-time **dashboard** with **SLA**, public satisfaction and budget.
    
-   Multi-phase scenario (Crisis Committee, Diagnosis, Mitigation, Communication, Closure).
    
-   Live **SIEM**\-like log panel and traffic chart.
    
-   Automatic generation of a forensic **PDF** report and **LaTeX** template for auditors.
    

---

### 1.6 Class usage & walkthrough (EN)

Suggested structure:

-   Use **Act 0** to discuss who should sit in a crisis **War Room** for this type of incident.
    
-   In **Act 1**, focus on reading the traffic chart and logs to decide if the issue is just legitimate load or a **DDoS**.
    
-   In **Act 2**, compare different mitigation strategies (**WAF**, **Scrubbing Center**, **Blackhole**) and their effect on users and budget.
    
-   In **Act 3**, ask students to draft a short public statement.
    
-   In **Act 4**, review the generated report as if you were an external regulator.
    

---

## 2\. CRISIS PROTOCOL: WAR ROOM

### 2.1 Descripción y objetivo (ES)

> **Objetivo didáctico principal:** entrenar al alumnado en **gestión de crisis** reputacional y de ciberseguridad, seleccionando el **equipo adecuado** para cada caso y entendiendo el equilibrio entre capacidades **técnicas**, **legales** y de **comunicación**.

Este simulador plantea una **War Room** corporativa que afronta decenas de incidentes:

-   **Ataques técnicos** (phishing, ransomware, DDoS…).
    
-   **Crisis de reputación** (campañas de activistas, comentarios masivos, **Fake News**, **Deepfake** del CEO).
    
-   **Problemas legales y regulatorios** (inspecciones de autoridad de datos, contratos de **SLA**, disputas sobre dominios).
    

Cada caso exige montar un mini **comité de crisis** con perfiles como:

-   Analista **SOC**, Admin de Sistemas, Jefe de Desarrollo.
    
-   Asesoría Legal, **DPO**, Dirección de Comunicación, **Community Manager**.
    

Las decisiones afectan dos métricas clave:

-   **Reputación**.
    
-   **Confianza** de clientes y grupos de interés.
    

---

### 2.2 Qué hace el código (ES)

La aplicación está construida como **SPA** en **HTML/CSS/JavaScript**, con diseño de **dashboard** y estética “retro grid”.

Componentes principales:

-   **Barra superior**
    
    -   Logo `PROTOCOL://WAR_ROOM`.
        
    -   Métricas de **REPUTACIÓN**, **CONFIANZA** y progreso de casos (`0/90`).
        
    -   Temporizador global de 40 minutos y botones de tema y reinicio.
        
-   **Panel izquierdo – Estado de misión**
    
    -   Resumen de la misión y estado actual.
        
    -   Selección de equipo por fase y visibilidad de la carga del **comité de crisis**.
        
-   **Panel central – Zona de casos**
    
    -   Cartas de amenaza (**threat-card**) con descripción narrativa de la situación.
        
    -   Rejilla de opciones (acciones posibles o combinaciones de perfiles).
        
    -   Motor interno que evalúa si el equipo elegido cumple los requisitos técnicos, legales y de comunicación (`req: {tech, legal, comms}`).
        
-   **Panel derecho – Registro de acciones**
    
    -   Log textual de decisiones tomadas y su impacto.
        
-   **Motor de juego (clase WarRoom)**
    
    -   Estado persistente (fase, reputación, confianza, caso actual), guardado en **localStorage** para reanudar partidas.
        
    -   Base de datos de 90 casos con: descripción, requisitos, mensaje de fallo y “lección” asociada.
        
    -   Generación de informe final en **PDF** (“Informe de Auditoría de Crisis”) con puntuación final y detalle de decisiones, mediante **jsPDF**.
        
        
-   **Sonido opcional**
    
    -   Motor **AudioSynth** basado en **Web Audio API** para música ambiente, activable desde el botón de altavoz.
        

---

### 2.3 Uso en el aula (ES)

1.  **Introducción al concepto de War Room**
    
    -   Explicar qué es una **War Room** de crisis: sala (física o virtual) donde se reúnen los roles clave.
        
    -   Presentar los perfiles disponibles: **SOC**, desarrollo, sistemas, legal, **DPO**, comunicación, negocio.
        
2.  **Demostración con 2–3 casos iniciales**
    
    -   Proyectar el simulador y resolver en plenario varios casos, por ejemplo:
        
        -   **Deepfake** del CEO anunciando el cierre de la empresa.
            
        -   Caída de proveedor cloud que afecta al servicio.
            
    -   Pedir al alumnado que argumente qué combinación de perfiles es necesaria.
        
3.  **Trabajo por equipos**
    
    -   Dividir la clase en grupos. Cada grupo juega una parte de los 90 casos.
        
    -   Para cada caso, deben:
        
        1.  Leer la situación.
            
        2.  Seleccionar equipo.
            
        3.  Ver resultado y leer la “lección” asociada.
            
        4.  Apuntar en una hoja qué han aprendido.
            
4.  **Debriefing**
    
    -   Compartir casos especialmente interesantes (por ejemplo, inspección de la **AEPD**, **Fake News**, fuga de datos interna).
        
    -   Discutir patrones:
        
        -   ¿Cuándo es imprescindible **legal**?
            
        -   ¿Cuándo se necesita liderar desde Comunicación?
            
        -   ¿En qué casos basta con reforzar la parte técnica?
            
5.  **Informe final**
    
    -   Generar el **PDF** de auditoría.
        
    -   Analizar, en clave de **post-mortem**, qué decisiones fueron sistemáticamente débiles (por ejemplo, infravalorar comunicación).
        

---

### 2.4 Resolución orientativa (ES)

El docente puede usar los siguientes principios para guiar la discusión, sin necesidad de memorizar los 90 casos:

-   **Regla de las tres columnas**
    
    -   Cada caso debe leerse como combinación de tres ejes:
        
        -   ¿Predomina el problema **técnico**?
            
        -   ¿Hay implicaciones **legales/regulatorias** claras?
            
        -   ¿Es principalmente un problema de **reputación/comunicación**?
            
-   **Ejemplos tipo**
    
    -   **Deepfake del CEO**
        
        -   Equipo recomendado: Dir. Comunicación, Asesoría Legal, Analista SOC.
            
        -   Mensaje clave: crisis de reputación + posible delito.
            
    -   **Inspección de autoridad de datos**
        
        -   Equipo recomendado: **DPO** / legal, quizá apoyo técnico para explicar logs.
            
        -   Evitar presencia de demasiados perfiles técnicos que confundan el proceso.
            
    -   **Ataque de bots en blog corporativo**
        
        -   Equipo recomendado: técnico (filtros) + **Community Manager**.
            
        -   Foco en frenar el daño reputacional, no solo el tráfico.
            
-   **Criterio de evaluación**
    
    -   Mantener **Reputación** y **Confianza** por encima de un umbral acordado (por ejemplo, 70–80 %) sin bloquear todos los riesgos a base de medidas desproporcionadas.
        

---

### 2.5 Overview (EN)

**CRISIS PROTOCOL: WAR ROOM** is a corporate-style crisis management simulator:

-   Students build an ad-hoc **crisis committee** for each of ~90 cases.
    
-   Each scenario encodes the required mix of **technical**, **legal** and **communications** skills.
    
-   Wrong teams lead to reputation and trust loss, but also show a short **lesson learned** for debriefing.
    
-   At the end, a **PDF** crisis audit report is generated for discussion.
    

---

### 2.6 Class usage & walkthrough (EN)

-   Use the first cases as a **guided exercise** to calibrate how the class reads the scenarios.
    
-   Highlight how some incidents are mostly **technical**, some mostly **legal/compliance**, and some mainly **reputational**.
    
-   Encourage students to justify team selection as if they were explaining it to a board or regulator.
    
-   Use the final report as a basis for a **post-mortem** session:
    
    -   Which areas were systematically under-represented?
        
    -   Did they underestimate communication in any major incident?
        

---

## 3\. DATA LEAK RESPONSE: CISO CENTER

### 3.1 Descripción y objetivo (ES)

> **Objetivo didáctico principal:** simular la respuesta integral a una **fuga de datos** personales bajo **RGPD/GDPR**, desde la investigación técnica hasta la decisión de notificar a la **AEPD** y a las personas afectadas, generando un informe formal.

Escenario de partida:

-   Se detecta una transferencia **anómala y masiva** (≈500 MB) de datos cifrados desde servidores de Finanzas hacia una IP en Europa del Este.
    
    
-   El riesgo potencial incluye:
    
    -   Exfiltración de datos personales.
        
    -   Sanciones multimillonarias por **RGPD**.
        
    -   Daño reputacional grave.
        

El alumnado, en el rol de **CISO**, debe:

1.  Formar un comité de crisis (CISO, **DPO**, legal externo, Analista **SOC**, Jefe de Sistemas, Dir. Comunicación, negocio).
    
2.  Analizar registros en una consola tipo **SIEM** para entender qué se ha perdido.
    
    
3.  Valorar **volumen**, **sensibilidad** y **riesgo** para los derechos y libertades de las personas.
    
4.  Decidir si la organización está obligada a notificar a la **AEPD** y a los afectados dentro del plazo de 72 horas.
    
5.  Redactar un informe en **PDF** que documente cronología, decisión y medidas de mitigación.
    

---

### 3.2 Qué hace el código (ES)

El simulador se estructura en **actos** y está implementado como **SPA** en **HTML/CSS/JavaScript**, con un diseño similar a un **CISO Center** corporativo.

Elementos principales:

-   **Barra superior**
    
    -   Logo `LEAK::RESPONSE`.
        
    -   Métricas dinámicas:
        
        -   Tiempo de fuga (`T. FUGA`).
            
        -   Datos afectados.
            
        -   Gravedad.
            
        -   Estado del incidente.
            
-   **Panel izquierdo – Recursos**
    
    -   Lista de perfiles disponibles con coste y competencias (técnicas, legales, comunicación).
        
        
-   **Panel central – Pantalla principal**
    
    -   Contenido dinámico según acto:
        
        -   **Acto 0 – Comité de crisis**: briefing de inteligencia y selección de equipo.
            
            
        -   **Acto 1 – Análisis forense**: vista tipo **SIEM** con logs de transferencia, accesos sospechosos, etc.
            
            
        -   **Acto 2 – Evaluación de impacto**:
            
            -   Texto explicativo sobre **RGPD**, **AEPD**, datos sensibles y plazo de 72h.
                
            -   Controles de selección (volumen, sensibilidad) y cálculo de riesgo.
                
        -   **Acto 3 – Informe**: editor asistido de secciones con frases predefinidas para construir el informe final.
            
-   **Panel derecho – Consola de eventos**
    
    -   Log textual de acciones y cambios de estado del incidente.
        
-   **Motor de simulación (clase DataLeakSim)**
    
    -   Estado con acto actual, equipo seleccionado, evidencias, severidad y tamaño de la fuga.
        
    -   **Timer** que incrementa el tiempo de fuga en bloques de 5 minutos de simulación.
        
    -   Glosario específico del acto 2 con términos clave de protección de datos (**RGPD**, **AEPD**, “Datos Sensibles”, “Derechos y Libertades”).
        
    -   Generación de informe en **PDF** mediante **jsPDF**.
        

---

### 3.3 Uso en el aula (ES)

1.  **Contextualización legal y técnica**
    
    -   Explicar brevemente **RGPD/GDPR**, el papel de **AEPD**, **DPO** y **CISO**.
        
    -   Introducir la diferencia entre “incidente de seguridad” y “brecha de datos personales”.
        
2.  **Acto 0 – Comité de crisis**
    
    -   Pedir al alumnado que configure un equipo máximo (por ejemplo, 4 perfiles) en función del briefing.
        
    -   Debatir por qué, en fugas de datos, la presencia del **DPO** y perfiles legales suele ser obligatoria.
        
3.  **Acto 1 – Análisis forense**
    
    -   Explorar los logs de la consola: origen/destino de la exfiltración, tipo de datos, indicios de **malware** o errores de configuración.
        
    -   Identificar qué evidencias son relevantes para la valoración de riesgo (no sólo para la parte técnica).
        
4.  **Acto 2 – Evaluación de impacto y decisión**
    
    -   Ajustar los selectores de volumen y sensibilidad y observar cómo cambia el indicador de **riesgo**.
        
        
    -   Discutir:
        
        -   ¿Cuándo es obligatorio notificar a la **AEPD**?
            
        -   ¿Cuándo se puede justificar documentar internamente sin notificación?
            
5.  **Acto 3 – Informe final**
    
    -   Construir, en grupo, un informe que incluya:
        
        -   Resumen ejecutivo en lenguaje no técnico.
            
        -   Descripción técnica de la exfiltración.
            
        -   Matriz de impacto y decisión de notificación.
            
        -   Plan de medidas correctoras y preventivas.
            

---

### 3.4 Resolución orientativa (ES)

Para el caso base de exfiltración de 500 MB de datos cifrados desde Finanzas hacia una IP desconocida:

1.  **Equipo recomendado**
    
    -   CISO (liderazgo técnico-estratégico).
        
    -   **DPO** (interpretación **RGPD/GDPR** y relación con **AEPD**).
        
    -   Analista **SOC** (análisis de logs y correlación).
        
    -   Jefe de Sistemas (acceso a servidores y **backup**).
        
    -   Dir. Comunicación (si se prevé impacto reputacional).
        
2.  **Análisis forense mínimo**
    
    -   Comprobar qué tablas o sistemas se han visto afectados (clientes, nóminas, etc.).
        
    -   Determinar si los datos son **personales** y si incluyen categorías de **datos sensibles**.
        
3.  **Evaluación de impacto**
    
    -   Volumen alto + datos potencialmente sensibles → **riesgo alto** para derechos y libertades.
        
4.  **Decisión de notificación**
    
    -   En este escenario, la decisión orientativa es:
        
        -   Notificar a la **AEPD** dentro de las 72 horas desde la detección.
            
        -   Notificar a las personas afectadas, describiendo medidas técnicas y organizativas adoptadas.
            
5.  **Informe**
    
    -   El **PDF** final debería dejar claro:
        
        -   La **línea temporal** del incidente.
            
        -   La base jurídica de la decisión.
            
        -   Las medidas de contención y los planes de prevención futuros.
            

---

### 3.5 Overview (EN)

**DATA LEAK RESPONSE: CISO CENTER** is a browser-based simulation of a personal data **breach** under **GDPR**:

-   Students build a crisis team (CISO, **DPO**, legal, SOC, systems, communications, business).
    
-   They analyse log data, evaluate **risk** and **impact** on data subjects and decide whether to notify the **supervisory authority** and the affected individuals.
    
-   A structured **PDF** report is produced for debriefing.
    

---

### 3.6 Class usage & walkthrough (EN)

-   Use **Act 0** to discuss who must be around the table for a **data breach**.
    
-   In **Act 1**, focus on which log entries are relevant for a GDPR-style assessment.
    
-   In **Act 2**, show that notification decisions are **risk-based**, not purely technical.
    
-   In **Act 3**, build an executive-level report and ask students to defend their decision as if they were in front of a regulator.
    

---

## 4\. Licencia

Este conjunto de materiales (código de los simuladores y este `README`) se publica bajo **licencia MIT**.

En términos prácticos:

-   Puedes usar, copiar y modificar el código para fines docentes o profesionales.
    
-   Puedes integrarlo en tus propios proyectos, incluso comerciales.
    
-   Debes conservar el aviso de copyright y el texto completo de la licencia.
    

Ejemplo de cabecera estándar:

```text
MIT License

Copyright (c) ...

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

Incluye el archivo `LICENSE` con el texto completo de la licencia en el repositorio.

---

## 5\. Glosario de términos

> Términos técnicos o en inglés usados en este `README` y en los simuladores, explicados en castellano.

-   **AEPD (Agencia Española de Protección de Datos)**  
    Autoridad de control española encargada de supervisar el cumplimiento del **RGPD/GDPR** y de recibir notificaciones de brechas de datos personales.
    
-   **AudioSynth**  
    Pequeño motor de generación de sonido implementado en **JavaScript** sobre **Web Audio API**, utilizado para crear música de fondo sintética en el simulador **WAR ROOM**.
    
-   **Backup**  
    Copia de seguridad de datos o sistemas que permite restaurar la información en caso de incidente (por ejemplo, ransomware o borrado accidental).
    
-   **Blackhole (Blackhole Routing)**  
    Técnica de mitigación de ataques **DDoS** consistente en desviar todo el tráfico hacia una “ruta agujero negro” donde se descarta, bloqueando tanto tráfico malicioso como legítimo.
    
-   **Brecha de datos (Data Breach)**  
    Incidente de seguridad en el que se produce acceso, destrucción, alteración o divulgación no autorizada de datos personales.
    
-   **Canvas**  
    Elemento de **HTML5** que permite dibujar gráficos en píxeles (por ejemplo, topologías o líneas de tráfico) mediante **JavaScript**.
    
-   **CISO (Chief Information Security Officer)**  
    Responsable máximo de la seguridad de la información en una organización, con una visión estratégica y de gobierno.
    
-   **CISO Center**  
    Denominación del panel central en el simulador de fuga de datos, que simula una sala de mando de un **CISO** con métricas e información consolidada.
    
-   **Chart.js**  
    Librería de **JavaScript** para crear gráficos interactivos (líneas, barras, etc.). En estos simuladores se utiliza para representar curvas de tráfico o indicadores.
    
-   **Command Center**  
    Concepto de “centro de mando” desde el que se monitoriza el estado de un sistema o crisis y se toman decisiones en tiempo real.
    
-   **Community Manager**  
    Perfil de comunicación encargado de gestionar comunidades y **redes sociales** de la organización, moderando comentarios y gestionando crisis en línea.
    
-   **CSS (Cascading Style Sheets)**  
    Lenguaje de estilos que define la apariencia de una página web: colores, tamaños, tipografías y disposición de elementos.
    
-   **DDoS (Distributed Denial of Service)**  
    Ataque de denegación de servicio distribuido en el que muchos equipos o bots generan tráfico masivo para saturar un servicio y hacerlo inaccesible.
    
-   **Deepfake**  
    Contenido de vídeo o audio manipulado mediante técnicas de inteligencia artificial para hacer creer que una persona ha dicho o hecho algo que nunca ocurrió.
    
-   **Dashboard**  
    Panel de control visual que reúne diferentes indicadores (**KPI**) y vistas (gráficos, logs, paneles) para dar una visión global de la situación.
    
-   **Datos Sensibles**  
    Categorías especiales de datos personales (salud, ideología, biometría, etc.) que reciben una protección reforzada bajo el **RGPD**.
    
-   **DPO (Data Protection Officer / Delegado de Protección de Datos)**  
    Figura obligatoria en muchas organizaciones, responsable de supervisar el cumplimiento de la normativa de protección de datos y de actuar como punto de contacto con la autoridad.
    
-   **Exfiltración**  
    Salida ilegítima de información desde el interior de una red hacia el exterior, normalmente de forma oculta.
    
-   **Fake News**  
    Noticias falsas o engañosas difundidas con intención de manipular la opinión pública o dañar la reputación de una organización o persona.
    
-   **FileSaver**  
    Librería de **JavaScript** que facilita la descarga de ficheros generados en el navegador (por ejemplo, archivos **PDF** o **ZIP**).
    
-   **Firewall**  
    Dispositivo o software que filtra tráfico de red según reglas (permitir o bloquear conexiones) para proteger sistemas internos.
    
-   **FrontEnd / Frontend**  
    Parte de una aplicación que se ejecuta en el navegador del usuario y con la que se interactúa directamente (interfaz, botones, formularios).
    
-   **GDPR (General Data Protection Regulation)**  
    Nombre en inglés del **RGPD**: reglamento europeo de protección de datos que establece obligaciones estrictas sobre tratamiento y brechas de datos personales.
    
-   **Hashtag**  
    Etiqueta precedida por `#` usada en **redes sociales** para agrupar conversaciones sobre un tema (por ejemplo, `#UCMCaida`).
    
-   **HTML (HyperText Markup Language)**  
    Lenguaje de marcado que define la estructura básica de una página web.
    
-   **HTTP 503**  
    Código de estado **HTTP** que indica que el servidor no puede atender la petición temporalmente, frecuentemente por saturación o mantenimiento.
    
-   **Impacto**  
    Resultado o consecuencia de un incidente: económico, reputacional, legal o sobre las personas afectadas.
    
-   **Infostealer**  
    Tipo de **malware** diseñado específicamente para robar información (credenciales, cookies, datos de navegador, etc.) de los equipos comprometidos.
    
-   **ISP (Internet Service Provider)**  
    Proveedor de servicios de Internet que da conectividad a la organización; en entornos académicos se coordina con redes como **RedIRIS**.
    
-   **JavaScript**  
    Lenguaje de programación principal en la web para dotar de lógica e interactividad a las páginas.
    
-   **JSZip**  
    Librería de **JavaScript** que permite crear archivos comprimidos (formato ZIP) directamente en el navegador.
    
-   **jsPDF**  
    Librería de **JavaScript** que permite generar documentos **PDF** desde el navegador sin necesidad de servidor.
    
-   **KPI (Key Performance Indicator)**  
    Indicador clave de rendimiento. En estos simuladores se usan, por ejemplo, **SLA**, reputación o satisfacción como KPI.
    
-   **LaTeX**  
    Sistema de composición de textos usado especialmente para documentos técnicos y científicos. Aquí se genera una plantilla LaTeX a partir de los datos del simulador.
    
-   **LocalStorage**  
    Mecanismo de almacenamiento local del navegador que permite guardar datos clave-valor en el dispositivo del usuario entre sesiones.
    
-   **Malware**  
    Término genérico para software malicioso (virus, troyanos, ransomware, etc.) que busca dañar sistemas o robar información.
    
-   **PDF (Portable Document Format)**  
    Formato de documento electrónico independiente de plataforma, común para informes oficiales y documentos finales.
    
-   **Phishing**  
    Técnica de engaño mediante correos o mensajes que imitan a entidades legítimas para robar credenciales u otra información sensible.
    
-   **Post-mortem**  
    Análisis realizado después de un incidente para entender qué ocurrió, qué se hizo bien o mal y cómo mejorar en el futuro.
    
-   **Redes Sociales (Social Media)**  
    Plataformas en línea (Twitter/X, Instagram, etc.) donde los usuarios publican y comparten contenido; clave en la gestión de reputación.
    
-   **RedIRIS**  
    Red académica y de investigación española que provee conectividad avanzada a universidades y centros de investigación; en el simulador, un actor clave para mitigación **DDoS**.
    
-   **Reputación**  
    Percepción que tienen clientes, usuarios y público en general sobre una organización; en el simulador se mide como porcentaje y se ve afectada por las decisiones.
    
-   **RGPD (Reglamento General de Protección de Datos)**  
    Normativa europea que regula el tratamiento de datos personales y las obligaciones ante una **brecha de datos**.
    
-   **Riesgo**  
    Combinación de la probabilidad de que ocurra un evento y el impacto que tendría. En el contexto del simulador de fuga de datos, se enfoca en el riesgo para los derechos y libertades de las personas.
    
-   **Scrubbing Center**  
    Servicio especializado, normalmente ofrecido por un **ISP** o red académica, que limpia el tráfico de ataque **DDoS** antes de reenviarlo al cliente.
    
-   **Severidad**  
    Medida de gravedad de un incidente, que ayuda a priorizar esfuerzos y a decidir si es necesario notificar a autoridades o afectados.
    
-   **SIEM (Security Information and Event Management)**  
    Plataforma que centraliza y correlaciona logs de múltiples sistemas de seguridad para facilitar la detección y análisis de incidentes.
    
-   **Single Page Application (SPA)**  
    Arquitectura web en la que toda la aplicación se carga en una única página y el contenido se actualiza dinámicamente sin recargar la página completa.
    
-   **SLA (Service Level Agreement)**  
    Acuerdo de nivel de servicio que define, normalmente en porcentaje, la disponibilidad esperada de un servicio (por ejemplo, 99,9 % de tiempo en línea).
    
-   **SOC (Security Operations Center)**  
    Centro de operaciones de seguridad. Equipo encargado de monitorizar continuamente sistemas y responder a incidentes.
    
-   **SQL Injection (SQLi)**  
    Ataque que introduce comandos SQL maliciosos en entradas de usuario para manipular la base de datos.
    
-   **Timeline / Línea temporal**  
    Representación ordenada en el tiempo de los hitos de un incidente (detección, acciones tomadas, cierre), usada en informes forenses.
    
-   **Trust (Confianza)**  
    Confianza de clientes y usuarios en la organización; en el simulador **WAR ROOM** se modela como métrica que disminuye ante malas decisiones.
    
-   **UCM (Universidad Complutense de Madrid)**  
    Universidad pública española. En el simulador de **DDoS**, el incidente se sitúa en su portal de matrícula.
    
-   **UI (User Interface / Interfaz de Usuario)**  
    Conjunto de elementos con los que el usuario interactúa (botones, paneles, gráficos, formularios) en una aplicación.
    
-   **War Room**  
    Sala real o virtual en la que un equipo multidisciplinar gestiona una crisis, tomando decisiones coordinadas bajo presión.
    
-   **WAF (Web Application Firewall)**  
    Tipo de firewall especializado en proteger aplicaciones web, inspeccionando tráfico HTTP/HTTPS para bloquear ataques como **SQL Injection** o ciertos patrones de **DDoS**.
    
-   **Web Audio API**  
    API de navegador que permite generar y procesar audio de forma programática (por ejemplo, crear música sintética).
    
