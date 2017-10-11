# RAML-Documentation
RAML Documentation


How the process of RAML documentation works?
To understand this, lets first understand the architecture for different entities used under RAML documentation.
Process Flow among different entities in RAML structure:

RAML Documentation----> apis--assets_get_set_name.raml
                        ||      || --assets_get_set_records_by_id.raml
                        ||      || --assets_get_sub_records_by_id.raml
                        ||      || --human_get_set_name.raml
                        ||      || --human_get_set_records_by_id.raml
                        ||      || --human_get_sub_records_by_id.raml               
                        ||      || --machine_get_set_name.raml
                        ||      || --machine_get_set_records_by_id.raml
                        ||      || --machine_get_sub_records_by_id.raml
                        ||      ||                          
                      errors    entities--Assets
                                    --Human
                                    --Machine
                                    --Assets
                                    --all-entities.raml


PROJECT_NAME.raml   :  This file includes different raml files to define different entities.
                       In our example, a company can have assests, humans, machines etc. 
                       So, we will include at least 3 raml files in PROJECT_NAME.raml file.
                       /assets: !include PROJECT_NAME_ASSETS.raml                       
                       /human: !include PROJECT_NAME_HUMAN.raml
                       /machines: !include PROJECT_NAME_MACHINE.raml

                       These files will include reference to different schemas and example to be part of documentation.
                       These schema and examples are referenced by all-entities.raml file.
                       so, we would need to add reference to all-entities.raml as well in PROJECT_NAME.raml file.
                       types: !include apis/entities/all-entities.raml

PROJECT_NAME_ASSETS.raml  : There are different such kind of files. for ex, PROJECT_NAME_HUMAN.raml, PROJECT_NAME_MACHINE.raml.
                        This file will reference the API definitions.
                        Refer:
                        /name/: !include apis/assets_get_set_name.raml
                        /records/{id}/: !include apis/assets_get_set_records_by_id.raml
                        /records/{id}/get_sub_records: !include apis/assets_get_sub_records_by_id.raml


apis/assets_get_set_name.raml :  There will be a lot of such file for each API.
                          This file will point to some entity which are defined in "entities/all-entities.raml" file.
apis/entities/all-entities.raml : This file contains reference to the schema and example of API request and response.
                           Refer below example for "AssetsGetSetNameRequest" entity referenced in "apis/assets_get_set_name.raml" API  
                           file:
                           AssetsGetSetNameRequest:
                               schema: !include Assets/schemas/Request/AssetsGetSetNameRequest.json
                               example: !include Assets/examples/Request/AssetsGetSetNameRequest.json
                           AssetsGetSetNameResponse:
                               schema: !include Assets/schemas/Request/AssetsGetSetNameResponse.json
                               example: !include Assets/examples/Request/AssetsGetSetNameResponse.json

apis/entities/Assets/AssetsGetSetNameRequest.json
apis/entities/Assets/AssetsGetSetNameResponse.json
                         These kind of files include structure of API request and response in respect of schema and example for APIs
                         request and response.
