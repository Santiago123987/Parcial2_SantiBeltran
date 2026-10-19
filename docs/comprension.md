# Comprensión del diseño — Enunciado C
**Nombre:** Santiago Elias Beltran Moreno.
**Fecha:** 19/10/26

Responde con tus palabras, basándote en `docs/UML-final.md`. Respuestas
concisas (2–4 líneas por pregunta). Evidencia que entendiste el contrato
**antes** de programar.

---

### 1. Herencia y polimorfismo
¿Por qué `Curso` es una clase abstracta y no concreta? Menciona qué método
obliga a cada subclase a implementar y qué gana el sistema con eso.

> _Tu respuesta:_ Porque las clases abstractas permiten que los que la heredan puedan usar sus metodos de diferentes maneras dependiendo de como la necesiten implementar y no que todas deban usar el metodo del mismo modo. El metodo que Curso obliga a sus subclases a implementar es: dificultadEsperada(). Lo que el sistema gana es polimorfismo: se puede tener una lista de Curso y llamar a dificultadEsperada() en cada uno sin saber de que tipo es, y cada uno responde a su manera. Ademas, si se añade un tipo nuevo de curso, solo implementa el metodo y ya funciona con el resto del sistema

---

### 2. Composición vs. agregación
Explica la diferencia entre `PlanEstudios ◆— Curso` (composición) y
`Facultad ◇— PlanEstudios` (agregación). ¿Qué pasaría con los cursos si se
elimina el plan? ¿Y con los planes si se elimina la facultad?

> _Tu respuesta:_ La diferencia principal que encuentro es que la clase Curso depende enteramente de PlanEstudios, si se llega a borrar PlanEstudios, Curso deja de existir y tiene sentido porque los cursos se crean dentro del constructor del plan, mientras que los planes se crean afuera. Mientras que la relacion entre Facultad y PlanEstudios es diferente porque aun si no hay una facultad, el plan de estudios puede seguir existiendo independientemente. Si se elimina la facultad, PlanEstudios sigue existiendo

---

### 3. Asociación
En `Estudiante — Curso`, ¿quién es dueño de quién? ¿Por qué se modela como
N:M y no como composición?

> _Tu respuesta:_ Aqui ninguno es dueño del otro, las clases existen cada una por su lado pero si se pueden relacionar la una con la otra. El estudiante accede a los cursos y esa es su relacion. Si se modelara como composicion entonces si Estudiante fuera el padre, al borrar al estudiante tambien se borra al curso y como ya dije, ellas existen por separado, el curso puede existir sin el estudiante. Lo mismo pasaria si Curso fuera el padre, pero yo como estudiante puedo estar inscrito en la U y aun asi no tener ningun curso. En cambio es N:M porque un estudiante cursa varios cursos y un curso lo cursan varios estudiantes

---

### 4. Dependencia
¿Por qué `Recomendador` **depende** de `HistorialAcademico` en lugar de
**tenerlo** como atributo? ¿Qué ventaja tiene pasar el servicio como
parámetro?

> _Tu respuesta:_ Porque el Recomendador no guarda el historial como atributo, solo lo recibe en el metodo recomendar() y lo usa en ese momento. El HistorialAcademico recoge la información del estudiante y el Recomendador la usa en cierto instante para recomendar un tipo de curso. Pasar el servicio como parametro hace que Recomendador sirva para cualquier estudiante y no tener que crear un recomendador para cada estudiante individualmente.

---

### 5. Listas
En este proyecto se usan dos estructuras distintas:
- `int[] notas` en `Estudiante`
- `ArrayList<Curso>` en `PlanEstudios` y `Estudiante`

Explica por qué en cada caso se eligió esa estructura y no la otra. ¿Qué
pasa si el estudiante intenta registrar más notas que la capacidad del
arreglo?

> _Tu respuesta:_ Las notas van en un int[] porque se sabe cuantas notas máximo puede tener un estudiante, entonces un arreglo de tamaño fijo sirve. Los cursos van en un ArrayList porque no se sabe cuantos van a ser y este se agranda solo. Si el estudiante intenta registrar más notas de las que caben, no se guarda la nota y el contador no sube