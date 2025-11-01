---
layout: mermaid
title: Patient
permalink: /models/patient/
---

~~~mermaid
graph TD
  A[Start] --> B{Decision}
  B -->|Yes| C[OK]
  B -->|No| D[End]
~~~
