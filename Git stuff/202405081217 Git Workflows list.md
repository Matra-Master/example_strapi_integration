---
created: 20240508-1217
tags:
  - git
  - gitlab
  - github
---
[[Git_workflows_list.excalidraw]]
# Gitflow (legacy)

- Main - Historial oficial de releases
- Develop - Branch para integrar features
- Feature - Se mergean en develop
- Release - Grupo de features integradas en Develop que están listas para Main.
- Hotfix - Arreglos rápidos y mantenimiento directo sobre Main

Features nunca interactuan con Main.

Crear un branch Release inicia un "ciclo de release", en ese branch no puede haber features nuevas, sólo bugfixes, tareas de documentación y cosas así entran como commits válidos antes de mandar a Main.

Un Release se mergea al final del ciclo en Main, y se le asigna un tag a esa versión.

Al final del ciclo el Release vuelve a Develop para incorporar los fixes y demás.


# [Gitlab Flow](https://about.gitlab.com/topics/version-control/what-is-gitlab-flow/)

Versión simplificada del *Gitflow*, usa desarrollo basado en features, contenidas en _feature branches_ e _issue trackers_.

- Todas las features y bugfixes van a *main*, se la considera el default
- Se permiten branches _production_ y/o _stable_
- Refuerza un montón de [buenas prácticas](https://about.gitlab.com/topics/version-control/what-are-gitlab-flow-best-practices/)
- Un equipo decide cuántos branches de "pre-producción" pone entre main y _production_. (ej. main -> test -> acceptance -> production)

En los casos donde un equipo mantiene un API con versiones Gitlab Flow aconseja mantener branches release como `v1` y `v2` que se mantienen individualmente. El potencial que tiene es el de identificar bugs muy viejos fácilmente.
La *ventaja* que dice aportar es la de permitir a los devs mantener y colaborar varias versiones de un codebase a la vez. Bien aplicado reduce el _overhead_ que suele aparecer al mantener más de una versión de código a la vez.

# Trunk-based

La piedra angular del workflow es la _automatización de los procesos de testeo y revisión de código_, lo que permite usar un solo branch principal sobre el que se desarrollan features chicas y muy rápido. 
Comparando, los demás flows se basan en features de larga vida que aparecen en branches paralelos y recién al ser terminadas vuelven al _main_; en cambio, el main en trunk-based se asume que siempe es estable, funcional y listo para deployment.
Es el flow requerido si un equipo orientado al DevOps pretende implementar correctamente _continuous integration_.
El repo de un proyecto Trunk-based siempre tiene un flujo constante de commits en main, y cada uno es testeado para que sea buildeable.

Sus buenas prácticas son:
- Desarrollar features pequeñas. La idea es llevar código a producción muy rápido y facilitar la revisión de cambios nuevos.
- Implementar *Feature flags* para cualquier nueva feature, permitiendo que viva en producción sin ser funcional hasta que esté lista para su activación.
- Implementar testeos automatizados y comprehensivos. Los feature and unit tests van durante el desarrollo y los merges; los full-stack y end-to-end se corren en pipelines contra entornos de producción.
- Hacer code reviews inmediatos y sobre el código ya testeado por pasos anteriores. El enfoque está en optimizar o asegurar que cumplan la consigna, no en arreglar errores.
- Tener tres o menos branches activas todo el tiempo. Una vez que una branch corta mergea se borra.
- Mergear branches al menos una vez al día. Es un ejercicio que ayuda a tomar el ritmo rápido que requiere el workflow.
- Reducir el número de fases de congelado de código, o de etapas donde se dejan de hacer cambios a propósito para deployar los anteriores.
- Buildear rápido y ejecutar de inmediato. Se refiere al ejercicio de acelerar procesos de buildeo con técnicas de cache, y usar estrategias de testing performantes.


# Github Flow
# Forking Workflow (Legacy)

Es el workflow que se usa en los proyectos open-source en Github. Cuando querés colaborar en el repo de alguien más o hacer tu propia variante de una app hacés un _fork_ del repo completo y trabajás desde ahí. Luego podés devolver algunos cambios al repo padre.

En el caso de un workflow de desarrollo como los nuestros implica que cada dev tenga en su cuenta de github un fork del repo y trabaje ahí como quiera. Llevando luego features puntuales al repo principal mediante pull requests.


---
## Related Ideas:
* [[fleeting]]
* [Gitflow-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- [babelgroup - Cinco git workflows](https://www.babelgroup.com/es/Media/Blog/Abril-2021/Cinco-Git-Workflows-para-mejores-proyectos) -Link muerto-