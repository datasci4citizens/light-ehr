---
layout: mermaid
title: Mih/MolarCheck
permalink: /models/Mih/molarcheck/
---
~~~mermaid
graph LR
    subgraph MIH["MIH Case Fields"]
        mih_id[mih_id]
        patient_id[patient_id]
        diagnosis[diagnosis]
        start_date[start_date]
        end_date[end_date]
        user_id[user_id]
        pain_level[pain_level]
        sensitivity_field[sensitivity_field]
        stain[stain]
        aesthetic_discomfort[aesthetic_discomfort]
        user_observations[user_observations]
        specialist_observations[specialist_observations]
        image_id[image_id]
        created_at[created_at]
        updated_at[updated_at]
    end
    
    subgraph OMOP["OMOP CDM Tables"]
        subgraph CONDITION["CONDITION_OCCURRENCE"]
            condition_occurrence_id[condition_occurrence_id]
            person_id[person_id]
            condition_concept_id[condition_concept_id]
            condition_start_date[condition_start_date]
            condition_end_date[condition_end_date]
            provider_id[provider_id]
        end
        
        subgraph MEASUREMENT["MEASUREMENT"]
            value_as_number[value_as_number]
        end
        
        subgraph OBSERVATION["OBSERVATION"]
            value_concept_id1[value_as_concept_id]
            value_concept_id2[value_as_concept_id]
            value_concept_id3[value_as_concept_id]
            value_as_string1[value_as_string]
            value_as_string2[value_as_string]
            observation_datetime[observation_datetime]
        end
        
        subgraph FACT["FACT_RELATIONSHIP"]
            domain_concept_id[domain_concept_id_1/2]
        end
        
        subgraph META["METADATA / INTERNAL"]
            internal_control[internal control]
        end
    end
    
    mih_id --> condition_occurrence_id
    patient_id --> person_id
    diagnosis --> condition_concept_id
    start_date --> condition_start_date
    end_date --> condition_end_date
    user_id --> provider_id
    
    pain_level --> value_as_number
    
    sensitivity_field --> value_concept_id1
    stain --> value_concept_id2
    aesthetic_discomfort --> value_concept_id3
    user_observations --> value_as_string1
    specialist_observations --> value_as_string2
    created_at --> observation_datetime
    
    image_id --> domain_concept_id
    
    updated_at --> internal_control
    
    style MIH fill:#e1f5ff
    style OMOP fill:#fff4e1
    style CONDITION fill:#d4edda
    style MEASUREMENT fill:#cfe2ff
    style OBSERVATION fill:#fff3cd
    style FACT fill:#e7d4f5
    style META fill:#d1d1d1
~~~