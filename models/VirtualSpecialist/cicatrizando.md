---
layout: mermaid
title: VirtualSpecialist/Cicatrizando
permalink: /models/VirtualSpecialist/cicatrizando/
---
~~~mermaid
classDiagram
    direction LR

    class VirtualSpecialist {
        <<VirtualModel>>
        +specialist_id: Integer (Key)
        +specialist_name: String
        +user_id: Integer
        +birthday: Date (null=True)
        +speciality: String (null=True)
        +city: String (null=True)
        +state: String (null=True)
    }

    class Provider {
        <<OMOP Table>>
        +provider_id: Integer (PK, from specialist_id)
        +provider_name: String (from specialist_name)
        +provider_birthday: Date (from birthday)
        +provider_user_id: Integer (from user_id)
        +specialty_string: String (from speciality)
    }

    class Location {
        <<OMOP Table>>
        +location_id: Integer (PK, from specialist_id)
        +city: String (from city)
        +state: String (from state)
    }

    VirtualSpecialist --|> Provider : binds(row_provider)
    VirtualSpecialist --|> Location : binds(row_location)
~~~