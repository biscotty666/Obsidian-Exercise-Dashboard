---
extends: Default
---

Route:: {"type":"Select","options":{"valuesList":{},"sourceType":"ValuesListNotePath","valuesListNotePath":"fileClasses.conf/Routes.md","valuesFromDVQuery":""},"command":{"id":"insert__presetField__Route","icon":"list-plus","label":"Insert Route field"}}
Activity:: {"type":"Select","options":{"valuesList":{"1":"🚴","2":"🚶"},"sourceType":"ValuesList","valuesListNotePath":"","valuesFromDVQuery":""},"command":{"id":"insert__presetField__Activity","icon":"list-plus","label":"Insert Activity field"}}

Duration:: {"type":"Number","options":{"step":"1","min":"0"}}
Distance:: {"type":"Number","options":{"step":".1"}}
Note:: {"type":"Input","options":{}}
Image:: {"type":"Input","options":{}}
Link:: {"type":"Input","options":{},"command":{"id":"insert__presetField__Link","icon":"list-plus","label":"Insert Link field"}}
ActivityDate:: {"type":"Date","options":{"dateFormat":"YYYY-MM-DD","defaultInsertAsLink":"false"},"command":{"id":"insert__exercise__ActivityDate","icon":"list-plus","label":"Insert ActivityDate field"}}