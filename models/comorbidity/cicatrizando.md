---
layout: mermaid
title: Comorbidity/Cicatrizando
permalink: /models/comorbidity/cicatrizando/
---

~~~mermaid
graph LR
    %% Virtual Model
    VC[VirtualComorbidity]
    
    %% Virtual Fields
    VC --> comorbidity_id[comorbidity_id]
    VC --> patient_id[patient_id]
    VC --> specialist_id[specialist_id]
    VC --> comorbidity_type[comorbidity_type]
    
    %% OMOP Table
    OBS[Observation]
    
    %% Mappings to Observation
    comorbidity_id --> |observation_id<br/>KEY| OBS
    patient_id --> |person_id<br/>KEY| OBS
    specialist_id --> |provider_id<br/>KEY| OBS
    comorbidity_type --> |value_as_concept_id<br/>KEY| OBS
    
    %% Constant mappings (shown for completeness)
    CONST1[CID_COMORBIDITY<br/>const] -.-> |observation_concept_id| OBS
    CONST2[datetime.now<br/>const] -.-> |observation_date| OBS
    CONST3[CID_NULL<br/>const] -.-> |observation_type_concept_id| OBS
    
    %% Styling
    classDef virtualModel fill:#e1f5ff,stroke:#01579b,stroke-width:3px
    classDef virtualField fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    classDef omopTable fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    classDef constant fill:#ffebee,stroke:#c62828,stroke-width:1px,stroke-dasharray: 5 5
    
    class VC virtualModel
    class comorbidity_id,patient_id,specialist_id,comorbidity_type virtualField
    class OBS omopTable
    class CONST1,CONST2,CONST3 constant
~~~