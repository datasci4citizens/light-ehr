---
layout: mermaid
title: VirtualWound/Cicatrizando
permalink: /models/VirtualWound/cicatrizando/
---
~~~mermaid
graph LR
    %% Virtual Model
    VW[VirtualWound]
    
    %% Virtual Fields
    VW --> wound_id[wound_id]
    VW --> region[region]
    VW --> wound_type[wound_type]
    VW --> start_date[start_date]
    VW --> end_date[end_date<br/>nullable]
    VW --> is_active[is_active]
    VW --> image_id[image_id<br/>nullable]
    VW --> patient_id[patient_id]
    VW --> specialist_id[specialist_id]
    VW --> updated_at[updated_at]
    
    %% OMOP Tables
    COND[ConditionOccurrence]
    OBS[Observation<br/>Wound Region]
    WI[WoundImage]
    
    %% Mappings to ConditionOccurrence
    wound_id --> |condition_occurrence_id<br/>KEY| COND
    patient_id --> |person_id| COND
    specialist_id --> |provider_id| COND
    wound_type --> |condition_concept_id<br/>choicemap| COND
    start_date --> |condition_start_date| COND
    end_date --> |condition_end_date| COND
    is_active --> |condition_status_concept_id<br/>choicemap| COND
    
    %% Mappings to Observation (Region)
    patient_id --> |person_id<br/>KEY| OBS
    updated_at --> |observation_date| OBS
    region --> |value_as_concept_id<br/>choicemap| OBS
    wound_id --> |observation_event_id<br/>KEY| OBS
    
    %% Mappings to WoundImage
    image_id --> |image_id| WI
    wound_id --> |wound_id<br/>KEY| WI
    
    %% Constant mappings
    CONST1[CID_NULL<br/>const] -.-> |condition_type_concept_id| COND
    CONST2[CID_WOUND_LOCATION<br/>const] -.-> |observation_concept_id<br/>KEY| OBS
    CONST3[CID_PK_CONDITION_OCCURRENCE<br/>const] -.-> |obs_event_field_concept_id| OBS
    CONST4[CID_NULL<br/>const] -.-> |observation_type_concept_id| OBS
    
    %% Styling
    classDef virtualModel fill:#e1f5ff,stroke:#01579b,stroke-width:3px
    classDef virtualField fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    classDef virtualFieldNull fill:#fff9c4,stroke:#f57f17,stroke-width:2px,stroke-dasharray: 3 3
    classDef omopTable fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    classDef constant fill:#ffebee,stroke:#c62828,stroke-width:1px,stroke-dasharray: 5 5
    
    class VW virtualModel
    class wound_id,region,wound_type,start_date,is_active,patient_id,specialist_id,updated_at virtualField
    class end_date,image_id virtualFieldNull
    class COND,OBS,WI omopTable
    class CONST1,CONST2,CONST3,CONST4 constant
~~~