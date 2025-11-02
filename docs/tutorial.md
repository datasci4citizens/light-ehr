---
layout: page
title: New Model Tutorial
permalink: /docs/tutorial/
---

## Terms

### Application Model

Models handled by the applications, like wounds, medications, etc.

### OMOP Model

OMOP models mapped from the application model, like observation, measurement, etc.

### Extra Storage Concept
Extra models that store data from the application model not handled by OMOP.

## Naming

All folder/file names must follow the pattern: in lowercase, without spaces; use `-` to replace spaces.

## New Model

* Inside the folder model, it must have a subfolder for each **Application Model**. Create a subfolder if it does not exist yet.
* Create a markdown file (`.md`) for your model inside this folder. Each application can have its own file, and it is also possible to have shared models. Name the file with the application: `cicatrizando.md`, `lembramed.md`, etc. When the model is shared, it can have the name `shared.md`.
* The file starts with a header as the example:
~~~markdown
---
layout: mermaid
title: Patient/Cicatrizando
permalink: /models/patient/cicatrizando/
---
~~~
  * `layout` is always mermaid;
  * `title` is the name of the Application Model / the name of the application;
  * `permalink` is the path: `models/application-model/application/`

* After the header, write your model in Mermaid between `~~~mermaid` and `~~~` as the example:
<pre>
~~~mermaid
your model
~~~ 
</pre>

* Update the `index.md` in the root with a link to your model. The bullets hierarchical structure follows the folder's hierarchical structure.
* The link is in Markdown and will address the permalink, as in the example:
<pre>
* Patient
  * [Cicatrizando](models/patient/cicatrizando/)
</pre>