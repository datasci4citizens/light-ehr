---
layout: mermaid
title: VirtualPatient/Cicatrizando
permalink: /models/VirtualPatient/cicatrizando/
---
~~~mermaid
graph LR
    subgraph VP["VirtualPatient (Virtual Fields)"]
        patient_id["patient_id"]
        name["name"]
        bind_code["bind_code"]
        gender["gender"]
        birthday["birthday"]
        specialist_id["specialist_id"]
        hospital_registration["hospital_registration"]
        phone_number["phone_number"]
        weight["weight"]
        height["height"]
        accept_tcl["accept_tcl"]
        smoke_frequency["smoke_frequency"]
        drink_frequency["drink_frequency"]
        user_id["user_id"]
        updated_at["updated_at"]
    end

    subgraph Person["OMOP: Person Table"]
        p_person_id["person_id 🔑"]
        p_birth_datetime["birth_datetime"]
        p_gender_concept_id["gender_concept_id"]
        p_provider_id["provider_id"]
        p_care_site_reg["person_care_site_registration"]
        p_user_id["person_user_id"]
    end

    subgraph NonClinical["Custom: PatientNonClinicalInfos"]
        nc_person_id["person_id 🔑"]
        nc_name["name"]
        nc_bind_code["bind_code"]
        nc_phone["phone_number"]
        nc_accept_tcl["accept_tcl"]
    end

    subgraph MeasHeight["OMOP: Measurement (Height)"]
        mh_person_id["person_id 🔑"]
        mh_value["value_as_number"]
        mh_concept["measurement_concept_id 🔑<br/>(CID_HEIGHT)"]
        mh_date["measurement_date"]
    end

    subgraph MeasWeight["OMOP: Measurement (Weight)"]
        mw_person_id["person_id 🔑"]
        mw_value["value_as_number"]
        mw_concept["measurement_concept_id 🔑<br/>(CID_WEIGHT)"]
        mw_date["measurement_date"]
    end

    subgraph ObsSmoke["OMOP: Observation (Smoke)"]
        os_person_id["person_id 🔑"]
        os_concept["observation_concept_id 🔑<br/>(CID_SMOKE_FREQUENCY)"]
        os_value["value_as_concept_id"]
        os_date["observation_date"]
    end

    subgraph ObsDrink["OMOP: Observation (Drink)"]
        od_person_id["person_id 🔑"]
        od_concept["observation_concept_id 🔑<br/>(CID_DRINK_FREQUENCY)"]
        od_value["value_as_concept_id"]
        od_date["observation_date"]
    end

    %% Person table mappings
    patient_id -->|"row_person"| p_person_id
    birthday -->|"row_person"| p_birth_datetime
    gender -->|"row_person<br/>(choicemap)"| p_gender_concept_id
    specialist_id -->|"row_person"| p_provider_id
    hospital_registration -->|"row_person<br/>(nullable)"| p_care_site_reg
    user_id -->|"row_person<br/>(nullable)"| p_user_id

    %% Non-clinical info mappings
    patient_id -->|"row_nonclinicalinfos"| nc_person_id
    name -->|"row_nonclinicalinfos"| nc_name
    bind_code -->|"row_nonclinicalinfos"| nc_bind_code
    phone_number -->|"row_nonclinicalinfos<br/>(nullable)"| nc_phone
    accept_tcl -->|"row_nonclinicalinfos"| nc_accept_tcl

    %% Height measurement mappings
    patient_id -->|"row_height"| mh_person_id
    height -->|"row_height<br/>(nullable)"| mh_value
    updated_at -->|"row_height"| mh_date

    %% Weight measurement mappings
    patient_id -->|"row_weight"| mw_person_id
    weight -->|"row_weight<br/>(nullable)"| mw_value
    updated_at -->|"row_weight"| mw_date

    %% Smoke frequency observation mappings
    patient_id -->|"row_smoke_frequency"| os_person_id
    smoke_frequency -->|"row_smoke_frequency<br/>(choicemap, nullable)"| os_value
    updated_at -->|"row_smoke_frequency"| os_date

    %% Drink frequency observation mappings
    patient_id -->|"row_drink_frequency"| od_person_id
    drink_frequency -->|"row_drink_frequency<br/>(choicemap, nullable)"| od_value
    updated_at -->|"row_drink_frequency"| od_date

    style VP fill:#e1f5ff
    style Person fill:#fff4e1
    style NonClinical fill:#ffe1f5
    style MeasHeight fill:#e1ffe1
    style MeasWeight fill:#e1ffe1
    style ObsSmoke fill:#f5e1ff
    style ObsDrink fill:#f5e1ff
~~~