---
layout: mermaid
title: VirtualPatient/MolarCheck
permalink: /models/VirtualPatient/molarcheck/
---
~~~mermaid
graph LR
    subgraph PATIENT["Patient Fields"]
        patient_id[patient_id]
        name[name]
        birthday[birthday]
        email[email]
        city[city]
        state[state]
        neighborhood[neighborhood]
        phone_number[phone_number]
        is_allowed[is_allowed]
        accept_tcle[accept_tcle]
        highFever[highFever]
        premature[premature]
        deliveryProblems[deliveryProblems]
        lowWeight[lowWeight]
        deliveryType[deliveryType]
        brothersNumber[brothersNumber]
        consultType[consultType]
        deliveryProblemsTypes[deliveryProblemsTypes]
        created_at[created_at]
        updated_at[updated_at]
    end
    
    subgraph OMOP["OMOP CDM Tables"]
        subgraph PERSON["PERSON"]
            person_id[person_id]
            person_source_value[person_source_value<br/>name + email + phone]
            year_of_birth[year_of_birth]
            month_of_birth[month_of_birth]
            day_of_birth[day_of_birth]
        end
        
        subgraph LOCATION["LOCATION"]
            loc_city[city]
            loc_state[state]
            address_1[address_1]
        end
        
        subgraph CONDITION["CONDITION_OCCURRENCE"]
            cond_occ_id1[condition_occurrence_id]
            cond_person_id1[person_id]
            cond_concept_id1[condition_concept_id]
            cond_start_date1[condition_start_date]
            cond_type_concept1[condition_type_concept_id]
            
            cond_occ_id2[condition_occurrence_id]
            cond_person_id2[person_id]
            cond_concept_id2[condition_concept_id]
            cond_start_date2[condition_start_date]
            cond_type_concept2[condition_type_concept_id]
            
            cond_occ_id3[condition_occurrence_id]
            cond_person_id3[person_id]
            cond_concept_id3[condition_concept_id]
            cond_start_date3[condition_start_date]
            cond_type_concept3[condition_type_concept_id]
            
            cond_occ_id4[condition_occurrence_id]
            cond_person_id4[person_id]
            cond_concept_id4[condition_concept_id]
            cond_start_date4[condition_start_date]
            cond_type_concept4[condition_type_concept_id]
            
            cond_occ_id5[condition_occurrence_id]
            cond_person_id5[person_id]
            cond_concept_id5[condition_concept_id]
            cond_start_date5[condition_start_date]
            cond_type_concept5[condition_type_concept_id]
            
            cond_occ_id6[condition_occurrence_id]
            cond_person_id6[person_id]
            cond_concept_id6[condition_concept_id]
            cond_start_date6[condition_start_date]
            cond_type_concept6[condition_type_concept_id]
        end
        
        subgraph OBSERVATION["OBSERVATION"]
            obs_id[observation_id]
            obs_person_id[person_id]
            obs_concept_id[observation_concept_id]
        end
        
        subgraph VISIT["VISIT_OCCURRENCE"]
            visit_type[visit_concept_id]
        end
        
        subgraph UNDEFINED["UNMAPPED / UNCLEAR"]
            question1[? application control]
            question2[? consent tracking]
            question3[? audit metadata]
            question4[? audit metadata]
        end
    end
    
    patient_id --> person_id
    name --> person_source_value
    email --> person_source_value
    phone_number --> person_source_value
    birthday --> year_of_birth
    birthday --> month_of_birth
    birthday --> day_of_birth
    city --> loc_city
    state --> loc_state
    neighborhood --> address_1
    
    highFever --> cond_occ_id1
    highFever --> cond_person_id1
    highFever --> cond_concept_id1
    highFever --> cond_start_date1
    highFever --> cond_type_concept1
    
    premature --> cond_occ_id2
    premature --> cond_person_id2
    premature --> cond_concept_id2
    premature --> cond_start_date2
    premature --> cond_type_concept2
    
    deliveryProblems --> cond_occ_id3
    deliveryProblems --> cond_person_id3
    deliveryProblems --> cond_concept_id3
    deliveryProblems --> cond_start_date3
    deliveryProblems --> cond_type_concept3
    
    lowWeight --> cond_occ_id4
    lowWeight --> cond_person_id4
    lowWeight --> cond_concept_id4
    lowWeight --> cond_start_date4
    lowWeight --> cond_type_concept4
    
    deliveryType --> cond_occ_id5
    deliveryType --> cond_person_id5
    deliveryType --> cond_concept_id5
    deliveryType --> cond_start_date5
    deliveryType --> cond_type_concept5
    
    deliveryProblemsTypes --> cond_occ_id6
    deliveryProblemsTypes --> cond_person_id6
    deliveryProblemsTypes --> cond_concept_id6
    deliveryProblemsTypes --> cond_start_date6
    deliveryProblemsTypes --> cond_type_concept6
    
    brothersNumber --> obs_id
    brothersNumber --> obs_person_id
    brothersNumber --> obs_concept_id
    
    consultType --> visit_type
    
    is_allowed --> question1
    accept_tcle --> question2
    created_at --> question3
    updated_at --> question4
    
    style PATIENT fill:#e1f5ff
    style OMOP fill:#fff4e1
    style PERSON fill:#d4edda
    style LOCATION fill:#d4edda
    style CONDITION fill:#f8d7da
    style OBSERVATION fill:#fff3cd
    style VISIT fill:#d1ecf1
    style UNDEFINED fill:#ffeaa7
~~~