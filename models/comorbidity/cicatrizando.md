---
layout: mermaid
title: Comorbidity/Cicatrizando
permalink: /models/comorbidity/cicatrizando/
---

~~~mermaid
classDiagram
    direction LR
    class VirtualComorbidity {
        <<VirtualModel>>
        +comorbidity_id: Integer (Key)
        +patient_id: Integer
        +specialist_id: Integer
        +comorbidity_type: String
    }

    class Observation {
        <<OMOP Table>>
        +observation_id: Integer (PK, from comorbidity_id)
        +person_id: Integer (PK, from patient_id)
        +provider_id: Integer (PK, from specialist_id)
        +observation_concept_id: Integer (Constant: CID_COMORBIDITY)
        +value_as_concept_id: Integer (PK, from comorbidity_type)
        +observation_date: DateTime (Constant: datetime.datetime.now())
        +observation_type_concept_id: Integer (Constant: CID_NULL)
    }

    VirtualComorbidity --|> Observation : binds(row_observation)
~~~
