# Elastic Rules Repo

## Makefile build
  ```bash
    PROJECT_DIR='/Users/danielbrown/Documents/code/detection-rules-dwb'
    cd ${PROJECT_DIR}
    make clean
    make all
  ```

## generate-navigator
  ```bash
    ./env/detection-rules-build/bin/python -m detection_rules dev build-release --generate-navigator
  ```  
  
## Help menu
  ```bash
    ./env/detection-rules-build/bin/python -m detection_rules -h
  ```

## create-rule
  ### eql `./env/detection-rules-build/bin/python -m detection_rules create-rule rules/dwb/eql.toml`
    ```bash
      ./env/detection-rules-build/bin/python -m detection_rules create-rule rules/dwb/eql.toml

      Rule type (query, saved_query, machine_learning, eql, esql, threshold, threat_match, new_terms): eql
      actions (multi, comma separated): 
      alert_suppression: 
      author (required)  (multi, comma separated): dwb
      building_block_type: 
      description (required): dwb_description
      enabled: true
      event_category_override: 
      exceptions_list (multi, comma separated): 
      false_positives (multi, comma separated): 
      filters (multi, comma separated): 
      from: now-9m
      index (multi, comma separated): logs-*, endgame-*
      interval: 5m
      license: 
      max_signals: 
      meta: 
      name (required): eql_template
      note: 
      query (required): process where process.name == "bash"
      references (multi, comma separated): 
      related_integrations (multi, comma separated): 
      required_fields (multi, comma separated): 
      risk_score (required): 1
      risk_score_mapping (multi, comma separated): 
      rule_id [9a26b2e7-ba55-4ff2-ae60-b715a490da6d] ("n/a" to leave blank)  (required): 
      rule_name_override: 
      setup: 
      severity (required): low
      severity_mapping (multi, comma separated): 
      tags (multi, comma separated): dwb
      add mitre tactic? [y/N]: N
      throttle: 
      tiebreaker_field: 
      timeline_id: 
      timeline_title: 
      timestamp_field: 
      timestamp_override: 
      to: 
      ls -l rules/dwb
    ```
  ### query `./env/detection-rules-build/bin/python -m detection_rules create-rule rules/dwb/query.toml`
    ```bash
      ./env/detection-rules-build/bin/python -m detection_rules create-rule rules/dwb/query.toml
      Rule type (query, saved_query, machine_learning, eql, esql, threshold, threat_match, new_terms): query
      actions (multi, comma separated): 
      alert_suppression: 
      author (required)  (multi, comma separated): dwb
      building_block_type: 
      description (required): dwb_description
      enabled: true
      exceptions_list (multi, comma separated): 
      false_positives (multi, comma separated): 
      filters (multi, comma separated): 
      from: now-9m
      index (multi, comma separated): logs-*
      interval: 5m
      language (required): kuery
      license: 
      max_signals: 
      meta: 
      name (required): query_template
      note: 
      query (required): @timestamp:*
      references (multi, comma separated): 
      related_integrations (multi, comma separated): 
      required_fields (multi, comma separated): 
      risk_score (required): 1
      risk_score_mapping (multi, comma separated): 
      rule_id [e39dc4eb-934f-4a74-905d-041a6288012b] ("n/a" to leave blank)  (required): 
      rule_name_override: 
      setup: 
      severity (required): low
      severity_mapping (multi, comma separated): 
      tags (multi, comma separated): dwb
      add mitre tactic? [y/N]: 
      throttle: 
      timeline_id: 
      timeline_title: 
      timestamp_override: 
      to:
      ls -l rules/dwb
    ```  
  ### new_terms `./env/detection-rules-build/bin/python -m detection_rules create-rule rules/dwb/new_terms.toml`
    ```bash
      ./env/detection-rules-build/bin/python -m detection_rules create-rule rules/dwb/new_terms.toml
      ls -l rules/dwb
    ```
  
  ### threshold ``
    ```bash
      ./env/detection-rules-build/bin/python -m detection_rules create-rule rules/dwb/threshold.toml
      ls -l rules/dwb
    ```
  ### IOC ``
    ```bash
      ./env/detection-rules-build/bin/python -m detection_rules create-rule rules/dwb/eql.toml
      ls -l rules/dwb
    ```






























This will be used to connect to DL-36 and upload rules

```bash
(testing) C:\git\detection-rules-main>python -m detection_rules kibana --provider-name basic1 --kibana-url https://dl-us36-dev.kb.us-east-1.aws.found.io:9243/ --kibana-user detection_rules --kibana-password  upload-rule --rule-file "C:\git\detection-rules-main\rules\custom\xdr_network_security\fortigate\test-rule.toml"

█▀▀▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄   ▄      █▀▀▄ ▄  ▄ ▄   ▄▄▄ ▄▄▄
█  █ █▄▄  █  █▄▄ █    █   █  █ █ █▀▄ █      █▄▄▀ █  █ █   █▄▄ █▄▄
█▄▄▀ █▄▄  █  █▄▄ █▄▄  █  ▄█▄ █▄█ █ ▀▄█      █ ▀▄ █▄▄█ █▄▄ █▄▄ ▄▄█

Successful uploads:
  - 3c9c4d04-a408-4bbc-9f3c-8e1c56e55a45
```

```bash
python -m detection_rules kibana upload-rule -h

Kibana client:
Options:
  --space TEXT                 Kibana space
  -kp, --kibana-password TEXT
  -ku, --kibana-user TEXT
  --cloud-id TEXT
  -k, --kibana-url TEXT

Usage: detection_rules kibana upload-rule [OPTIONS]

  Upload a list of rule .toml files to Kibana.

Options:
  -f, --rule-file FILE
  -d, --directory DIRECTORY  Recursively export rules from a directory
  -id, --rule-id TEXT
  -r, --replace-id           Replace rule IDs with new IDs before export
  -h, --help                 Show this message and exit.
```

note the directory and replace id options.

Import rules from export

```bash
(testing) C:\git\detection-rules-main>python -m detection_rules import-rules -d rules/custom/ndjson
```

Add non-ECS fields to schema

```bash
(testing) C:\git\detection-rules-main>python -m detection_rules create-rule -t threshold rules/custom/xdr_server_security/glb_au_win_kerberos_password_spray_attempt.toml

█▀▀▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄▄▄ ▄   ▄      █▀▀▄ ▄  ▄ ▄   ▄▄▄ ▄▄▄
█  █ █▄▄  █  █▄▄ █    █   █  █ █ █▀▄ █      █▄▄▀ █  █ █   █▄▄ █▄▄
█▄▄▀ █▄▄  █  █▄▄ █▄▄  █  ▄█▄ █▄█ █ ▀▄█      █ ▀▄ █▄▄█ █▄▄ █▄▄ ▄▄█

actions (multi, comma separated):
alert_suppression:
author (required)  (multi, comma separated): Alex Dangel
building_block_type:
description (required): Kerberos Password Spray attempts
enabled: true
exceptions_list (multi, comma separated):
false_positives (multi, comma separated):
filters (multi, comma separated):
from: 15m
index (multi, comma separated): windows:*logs-wmic
interval: 5m
language (required): kuery
license:
max_signals: 100
meta:
name (required): GLB.AU.WIN Kerberos Password Spray Attempt
note:
query (required): event.code: ("4768" or "4771" or "4772") AND NOT winlog.event_data.Status: "0x0"  AND NOT user.name : *$* AND winlog.event_data.ServiceName : * AND source.ip : * AND winlog.event_data.ServiceName: * AND user.name : *
references (multi, comma separated):
related_integrations (multi, comma separated):
required_fields (multi, comma separated):
risk_score (required): 21
risk_score_mapping (multi, comma separated):
rule_id [37de77f6-5e69-47ee-ae89-c0ac464fd615] ("n/a" to leave blank)  (required): 262b369b-bb86-4567-a6d4-1ed8df3f7f2a
rule_name_override:
setup:
severity (required): low
severity_mapping (multi, comma separated):
tags (multi, comma separated): wmic, threshold, xdr_server_security
add mitre tactic? [y/N]: N
threshold cardinality (multi, comma separated): host.ip
threshold field (required)  (multi, comma separated): organization.id, user.name
threshold value (required): 1
throttle:
timeline_id:
timeline_title:
timestamp_override: event.ingested
to: now
```

Demo

1. Creating a simple query detection rule:

```bash
python -m detection_rules create-rule rules/custom/xdr_network_security/fortigate/glb_aa_net_fortigate_traffic_to_google.toml
```

Rule type (query, machine_learning, eql, threshold, threat_match, new_terms): query
actions (multi, comma separated):
alert_suppression:
author (required)  (multi, comma separated): Alex Dangel
building_block_type:
description (required): Alerts when traffic goes to 8.8.8.8 or 8.8.4.4
enabled: true
exceptions_list (multi, comma separated):
false_positives (multi, comma separated):
filters (multi, comma separated):
index (multi, comma separated): dl-*:logs-fortigate
interval: 15m
language (required): kuery
license:
max_signals: 100
meta:
name (required): [GLB.AA.NET](http://glb.aa.net/) Fortigate Traffic to Google
note:
query (required): destination.ip:(8.8.8.8 or 8.8.4.4)
references (multi, comma separated):
related_integrations (multi, comma separated):
required_fields (multi, comma separated):
risk_score (required): 21
risk_score_mapping (multi, comma separated):
rule_id [45d7a838-2f05-4d06-b46e-b8d1ac367fd3] ("n/a" to leave blank)  (required):
rule_name_override:
setup:
severity (required): low
severity_mapping (multi, comma separated):
tags (multi, comma separated): fortigate, xdr_network_security
add mitre tactic? [y/N]:
throttle:
timeline_id:
timeline_title:
timestamp_override: event.ingested
to: now

1. Uploading to Elastic:

```bash
python -m detection_rules kibana --provider-name basic1 --kibana-url https://dl-us36-dev.kb.us-east-1.aws.found.io:9243/ --kibana-user detection_rules --kibana-password VuuLf4zp3iBUGu9 upload-rule --rule-file "C:\git\detection-rules-main\rules\custom\xdr_network_security\fortigate\glb_aa_net_fortigate_traffic_to_google.toml"
```

1. Updating Rules:

Suppose we want to add our IPv6 addresses: 

```
2001:4860:4860:0:0:0:0:8888
2001:4860:4860:0:0:0:0:8844
```

Edit the TOML file and reupload. NOTE: new id will be assigned and now 2 rule versions will exist in Elastic

```bash
python -m detection_rules kibana --provider-name basic1 --kibana-url https://dl-us36-dev.kb.us-east-1.aws.found.io:9243/ --kibana-user detection_rules --kibana-password VuuLf4zp3iBUGu9 upload-rule -r --rule-file "C:\git\detection-rules-main\rules\custom\xdr_network_security\fortigate\glb_aa_net_fortigate_traffic_to_google.toml"
```

1. Bulk Import and Conversion from NDJSON export: