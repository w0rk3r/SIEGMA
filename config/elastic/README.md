# Elastic SIEM config

This folder holds the configuration file for a specific platform. An explanation of the fields is available below. 

## Fields that are worth looking into to adapt to your particular use case

| Elastic SIEM Config Field | Description                                                       | Example                                               | 
|---------------------------|-------------------------------------------------------------------|-------------------------------------------------------|
| from                      | No need to change if you're using `timeframe` in your Sigma rules | now-15m                                               |
| timeline_id               | Not included in the configuration but can be added                | "timeline_id":"e17d2870-6bb5-11ea-9871-d10df4e7cd14"  |
| timeline_title            | Not included in the configuration but can be added                | "timeline_title":"AWS CloudTrail"                     |
| sigma_params              | Used in conjunction with switch --sigma_extra_parameters. Dictionary under which any of the parameters supported by Sigma can be added. | {"sigma_params": {"--backend-option": ["key=value", "case_insensitive_whitelist=*"]}} |


## Elastic SIEM Configuration & Data Dictionary 

| Elastic SIEM Config Field  | Default Value         | Field type               | Description                                                                                                                           |
|----------------------------|-----------------------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| sigma_query_format         | es-qs                 | Hardcoded                | Preset value. This value is passed to sigmac                                                                                          |
| sigma_params               | N/A                   | User input optional      | Used in conjunction with switch --sigma_extra_parameters. Dictionary under which any of the parameters supported by Sigma can be added. Example: {"sigma_params": {"--backend-option": ["key=value", "case_insensitive_whitelist=*"]}} |
| kibana_username            | No default value      | User input optional      | Enables automatic rule upload if filled                                                                                               |
| kibana_password            | No default value      | User input optional      | Enables automatic rule upload if filled                                                                                               |
| kibana_url                 | No default value      | User input optional      | Enables automatic rule import if filled (i.e http://my_kibana:5601)                                                                   |
| rule_id                    | No default value      | Sigma: id                | Rule identifier                                                                                                                       |
| id                         | No default value      | Sigma: id                | Rule identifier                                                                                                                       |
| author                     | No default value      | Sigma: author            | Rule author                                                                                                                           |
| from                       | now-15m               | Sigma: timeframe         | Defines how much data in the past should be queried. Example: now-15m                                                                 |
| index                      | ["*"]                 | User input needed        | Define the indexes that should be queried. Example: filebeat-*                                                                        |
| interval                   | 5m                    | User input needed        | Define how often the rule should run in Elastic SIEM                                                                                  |
| language                   | kuery                 | Hardcoded                | Preset field and value. Don't change                                                                                                  |
| output_index               | .siem-signals-default | Hardcoded                | Default index used by Elastic SIEM                                                                                                    |
| references                 | No default value      | Sigma: references        | References and documentation related to the detection                                                                                 |
| false_positives            | No default value      | Sigma: falsepositives    | Event under which a false positive can trigger the detection                                                                          |
| risk_score                 | No default value      | Sigma: severity or score | Custom defined value in custom attribute/field "score" takes precedence. Otherwise, tag low=25, medium=50, high=75, critical=100      |
| name                       | No default value      | Sigma: title             | Rule name                                                                                                                             |
| note                       | No default value      | Sigma: note              | Contains relative path (from notes_folder) to a `.md` (markdown formatted) file with details for investigation guide / notes for a given detection use case. Optional field that can be set in config or rule.yml file. Settings in rule.yml take precedence over settings in config. |
| notes_folder               | No default value      | Sigma Config: notes_folder | Contains path to a folder that contains `.md` (markdown formatted) file containing details for investigation guide / notes for a given detection use case. Optional field that can be set either in config or using -co from commandline. |                                                                                                                             |
| description                | No default value      | Sigma: description       | Rule description                                                                                                                      |
| query                      | No default value      | Hardcoded                | Comes from the result of running sigmac                                                                                               |
| severity                   | No default value      | Sigma: severity          | Rule severity                                                                                                                         |
| tags                       | No default value      | Sigma: siemtags          | Tags to aid in rule identification                                                                                                    |
| to                         | now                   | Hardcoded                | Preset field and value. Don't change                                                                                                  |
| threshold.field            | null                  | Sigma: threshold.field   | Optional parent field. Used for aggregate based rules on Kibana. 'threshold' key can be skipped entirely. Value must be a "string" that can be mapped into ECS format based on the sigma config file 'fieldmappings' passed to SIEGMA. Same fields in the rule.yml file will take precendence over the values defined in siegma config |
| threshold.value            | null                  | Sigma: threshold.value   | Optional parent field. Used for aggregate based rules on Kibana to depict count. If events greater than equal to threshold.value are observed, rule will trigger. 'threshold' key can be skipped entirely. Value preferrably should be an "Integer". Same fields in the rule.yml file will take precendence over the values defined in siegma config |
| type                       | query                 | Hardcoded                | Preset field and value. Don't change                                                                                                  |
| threat                     | No default value      | Sigma: tags              | ATT&CK mapping                                                                                                                        |
| throttle                   | no_actions            | Hardcoded                | Preset field and value. Don't change                                                                                                  |
| timeline_id                | No default value      | Must be added to config  | SIEM Timeline ID (i.e e17d2870-6bb5-11ea-9871-d10df4e7cd14)                                                                           |
| timeline_title             | No default value      | Must be added to config  | Desired name to be associated with the Timeline (i.e AWS CloudTrail)                                                                  |
