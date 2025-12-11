---
layout: mermaid
title: VirtualSpecialist/MolarCheck
permalink: /models/VirtualSpecialist/molarcheck/
---
~~~mermaid
graph LR
    subgraph USER["User/Provider Fields"]
        id[id]
        name[name]
        email[email]
        city[city]
        state[state]
        neighborhood[neighborhood]
        phone_number[phone_number]
        is_allowed[is_allowed]
        accept_tcle[accept_tcle]
        created_at[created_at]
        updated_at[updated_at]
    end
    
    subgraph OMOP["OMOP CDM Tables"]
        subgraph PROVIDER["PROVIDER"]
            provider_id[provider_id]
            provider_name[provider_name]
            provider_source_value[provider_source_value]
        end
        
        subgraph LOCATION["LOCATION"]
            loc_city[city]
            loc_state[state]
            address_1[address_1]
        end
        
        subgraph UNDEFINED["UNMAPPED / UNCLEAR"]
            question1[? application control]
            question2[? consent tracking]
            question3[? audit metadata]
            question4[? audit metadata]
        end
    end
    
    id --> provider_id
    name --> provider_name
    email --> provider_source_value
    phone_number --> provider_source_value
    city --> loc_city
    state --> loc_state
    neighborhood --> address_1
    
    is_allowed --> question1
    accept_tcle --> question2
    created_at --> question3
    updated_at --> question4
    
    style USER fill:#e1f5ff
    style OMOP fill:#fff4e1
    style PROVIDER fill:#d4edda
    style LOCATION fill:#d4edda
    style UNDEFINED fill:#ffeaa7
~~~