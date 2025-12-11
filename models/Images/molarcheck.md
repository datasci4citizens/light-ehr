---
layout: mermaid
title: Images/MolarCheck
permalink: /models/Images/molarcheck/
---
~~~mermaid
graph LR
    subgraph IMAGE["Image Fields"]
        image_id[image_id]
        extension[extension]
        user_id[user_id]
        created_at[created_at]
        updated_at[updated_at]
    end
    
    subgraph OMOP["OMOP CDM Tables"]
        subgraph OBSERVATION["OBSERVATION"]
            observation_id[observation_id]
            value_as_string[value_as_string]
            provider_id[provider_id]
            observation_date[observation_date]
        end
        
        subgraph INTERNAL["NOT MAPPED"]
            not_mapped[internal metadata]
        end
    end
    
    image_id --> observation_id
    extension --> value_as_string
    user_id --> provider_id
    created_at --> observation_date
    updated_at --> not_mapped
    
    style IMAGE fill:#e1f5ff
    style OMOP fill:#fff4e1
    style OBSERVATION fill:#fff3cd
    style INTERNAL fill:#d1d1d1
~~~