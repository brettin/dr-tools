# Datarobot API tools

## Command line tools

The DataRobot tools require an authentication token. The `dr-login` script creates
a token that is stored in a file .datarobot_token in your home directory:

```
  $ dr-login usernamame password
  Got {"apiToken": "9XXXX-YYYYY"}
```

The list of active projects can be enumerated using `dr-list-projects`:

```
  $ dr-list-projects
  ID                       Name                                       Filename
  XXXXXXXXXXXXXXXXXXXXXXXX lesion_bio                                 lesion_data.csv
  XXXXXXXXXXXXXXXXXXXXXXXX lesion_bio_snp                             lesion_data.csv
  XXXXXXXXXXXXXXXXXXXXXXXX lesion_bio_snp_pmh_arrED_demo_subst_arrGCS lesion_data.csv
  XXXXXXXXXXXXXXXXXXXXXXXX severe_cluter_outcome                      severe_cluster_data.csv
  XXXXXXXXXXXXXXXXXXXXXXXX severe_clusters_no_mild                    severe_cluster_data.csv
  XXXXXXXXXXXXXXXXXXXXXXXX severe_clusters                            severe_cluster_data.csv
  XXXXXXXXXXXXXXXXXXXXXXXX api-test-tsb                               GDSC.193.tsv.binary.upload.robot.csv
  [...]
```

If you add a parameter to the `dr-list-projects` command it will limit the output to projects
with a name matching that parameter:

```
  $ dr-list-projects ANL
  ID                       Name                  Filename
  XXXXXXXXXXXXXXXXXXXXXXXX ANL PTSD 3.0 (Manual) PTSD_6mo_no_leak.csv
  XXXXXXXXXXXXXXXXXXXXXXXX ANL PTSD 2.0          PTSD_6mo_no_leak.csv
  XXXXXXXXXXXXXXXXXXXXXXXX ANL Demo PTSD 1.0     TRACKTBI_Pilot_DEID_02.22.18v2.csv
  XXXXXXXXXXXXXXXXXXXXXXXX ANL Demo 3.0          TRACKTBI_Pilot_DEID_02.22.18v2.csv
  XXXXXXXXXXXXXXXXXXXXXXXX ANL Demo 2.0          TRACKTBI_Pilot_DEID_02.22.18v2.2.csv
  XXXXXXXXXXXXXXXXXXXXXXXX ANL Demo 1.0          TRACKTBI_Pilot_DEID_02.22.18v2.2.csv
```

You can check the status of a particular project using the `dr-project-status` command:

```
  $ dr-project-status XXXXXXXXXXXXXXXXXXXXXXXX 
  {
     "stage" : "modeling",
     "stageDescription" : "Ready for modeling",
     "autopilotDone" : true
  }
```

You can upload data and create a new project using the `dr-create-project` command:

```
  $ perl dr-create-project x.csv bob-test-5
  Check status: http://140.221.10.250/api/v2/status/XX-YY-ZZ-QQ/
  Status: {"status": "RUNNING", "message": "", "code": 0, "created": "2018-04-10T21:00:59.637475Z"}
  Check status: http://140.221.10.250/api/v2/status/XX-YY-ZZ-QQ/
  Status: {"status": "RUNNING", "message": "", "code": 0, "created": "2018-04-10T21:00:59.637475Z"}
  Check status: http://140.221.10.250/api/v2/status/XX-YY-ZZ-QQ/
  Status: {"status": "RUNNING", "message": "", "code": 0, "created": "2018-04-10T21:00:59.637475Z"}
  Check status: http://140.221.10.250/api/v2/status/XX-YY-ZZ-QQ/
  Status: {"status": "RUNNING", "message": "", "code": 0, "created": "2018-04-10T21:00:59.637475Z"}
  Check status: http://140.221.10.250/api/v2/status/XX-YY-ZZ-QQ/
  Status: {"status": "RUNNING", "message": "", "code": 0, "created": "2018-04-10T21:00:59.637475Z"}
  Check status: http://140.221.10.250/api/v2/status/XX-YY-ZZ-QQ/
  Status: {"id": "XXXXXXXXXXXXXXXXXX", "projectName": "bob-test-5", "fileName": "x.csv", "stage": "aim", "autopilotMode": null, "created": "2018-04-10T21:01:04.941835Z", "target": null, "metric": null, "partition": {"datetimeCol": null, "cvMethod": null, "validationPct": null, "reps": null, "cvHoldoutLevel": null, "holdoutLevel": null, "userPartitionCol": null, "validationType": null, "trainingLevel": null, "partitionKeyCols": null, "holdoutPct": null, "validationLevel": null}, "recommender": {"recommenderItemId": null, "isRecommender": null, "recommenderUserId": null}, "advancedOptions": {"scaleoutModelingMode": "disabled", "responseCap": null, "downsampledMinorityRows": null, "downsampledMajorityRows": null, "blueprintThreshold": null, "seed": null, "weights": null, "smartDownsampled": false, "majorityDownsamplingRate": null}, "positiveClass": null, "maxTrainPct": null, "holdoutUnlocked": false, "targetType": null}
  Project ID found: XXXXXXXXXXXXXXXXXX
  Created: XXXXXXXXXXXXXXXXXX
```