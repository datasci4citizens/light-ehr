---
layout: mermaid
title: VirtualSpecialist/Cicatrizando
permalink: /models/VirtualSpecialist/cicatrizando/
---
~~~mermaid
graph LR
    %% Virtual Model
    VS[VirtualSpecialist]
    
    %% Virtual Fields
    VS --> specialist_id[specialist_id]
    VS --> specialist_name[specialist_name]
    VS --> user_id[user_id]
    VS --> birthday[birthday<br/>nullable]
    VS --> speciality[speciality<br/>nullable]
    VS --> city[city<br/>nullable]
    VS --> state[state<br/>nullable]
    
    %% OMOP Tables
    PROV[Provider]
    LOC[Location]
    
    %% Mappings to Provider
    specialist_id --> |provider_id<br/>KEY| PROV
    specialist_name --> |provider_name| PROV
    user_id --> |provider_user_id| PROV
    birthday --> |provider_birthday| PROV
    speciality --> |specialty_string| PROV
    
    %% Mappings to Location
    specialist_id --> |location_id<br/>KEY| LOC
    city --> |city| LOC
    state --> |state| LOC
    
    %% Styling
    classDef virtualModel fill:#e1f5ff,stroke:#01579b,stroke-width:3px
    classDef virtualField fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    classDef virtualFieldNull fill:#fff9c4,stroke:#f57f17,stroke-width:2px,stroke-dasharray: 3 3
    classDef omopTable fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    
    class VS virtualModel
    class specialist_id,specialist_name,user_id virtualField
    class birthday,speciality,city,state virtualFieldNull
    class PROV,LOC omopTable
~~~