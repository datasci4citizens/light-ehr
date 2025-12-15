---
layout: mermaid
title: VirtualTrackingRecords/MolarCheck
permalink: /models/VirtualTrackingRecords/molarcheck/
---
~~~mermaid
graph LR
    subgraph TRACK["Tracking Record Fields"]
        tracking_record_id[tracking_record_id]
        patient_id[patient_id]
        image_id[image_id]
        observations[observations]
        created_at[created_at]
        updated_at[updated_at]
    end
    
    subgraph OMOP["OMOP CDM Tables"]
        subgraph OBSERVATION["OBSERVATION"]
            observation_id[observation_id]
            person_id[person_id]
            value_as_string[value_as_string]
            observation_date[observation_date]
        end
        
        subgraph FACT["FACT_RELATIONSHIP"]
            fact_relation[image relationship]
        end
        
        subgraph INTERNAL["NOT MAPPED"]
            not_mapped[internal control only]
        end
    end
    
    tracking_record_id --> observation_id
    patient_id --> person_id
    image_id --> fact_relation
    observations --> value_as_string
    created_at --> observation_date
    updated_at --> not_mapped
    
    style TRACK fill:#e1f5ff
    style OMOP fill:#fff4e1
    style OBSERVATION fill:#fff3cd
    style FACT fill:#e7d4f5
    style INTERNAL fill:#d1d1d1
~~~