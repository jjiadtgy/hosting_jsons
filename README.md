# Hosting JSONs

- Objective make each of couple input / expected work
- You can directly retrieve it via API using `Raw` feature from GitHub (for example [this](https://raw.githubusercontent.com/jjiadtgy/hosting_jsons/main/JSelectKeyExecuteStepTest/ut1/input.json))
- Table parameters for each unit tests

| JParsingStep   | UT  | Parameters                                                                                        |
|----------------|-----|---------------------------------------------------------------------------------------------------|
| JSelectKey     | ut1 | JSelectKey(selectedKeysAre = Array("col_nominal_struct", "col_nominal", "col_not.nominal_struct") |
|                | ut2 | JSelectKey(selectedKeysAre = Array("col_non_existing")                                            |
| JSelectStruct  | ut1 | JSelectStruct("col_applyOn", selectedKeysAre = Array("sub2", "sub0"))                             |
|                | ut2 | JSelectStruct("col.applyOn", selectedKeysAre = Array("sub.0"))                                    |
|                | ut3 | SelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array("col_duplicated"))                  |
|                | ut4 | JSelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array("sub0"), keep = true)              |
|                | ut5 | JSelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array.empty)                             |
|                | ut6 | JSelectStruct(applyOn = "NotExist", selectedKeysAre = Array("sub0"))                              |
|                | ut7 | JSelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array("NotExist"))                       |
|                | ut8 | JSelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array("sub0"))                           |
| JSelectArray   | ut1 | JSelectArray("col_applyOn", 1)                                                                    |
|                | ut2 | JSelectArray("col_applyOn", -1)                                                                   |
|                | ut3 | JSelectArray("col_applyOn", 0, keep = true)                                                       |
|                | ut4 | JSelectArray("NotExist", 0)                                                                       |
|                | ut5 | JSelectArray("col_applyOn", 0)                                                                    |
| JExplodeStruct | ut1 | JExplodeStruct("col_applyOn")                                                                     |
|                | ut2 | JExplodeStruct("col.applyOn")                                                                     |
|                | ut3 | JExplodeStruct("col_applyOn")                                                                     |
|                | ut4 | JExplodeStruct("col_applyOn", keep = true)                                                        |
|                | ut5 | JExplodeStruct("col_applyOn")                                                                     |
|                | ut6 | JExplodeStruct("NotExist")                                                                        |
|                | ut7 | JExplodeStruct("col_applyOn")                                                                     |
| JExplodeArray  | ut1 | JExplodeArray("col_applyOn")                                                                      |
|                | ut2 | JExplodeArray("col_applyOn")                                                                      |
|                | ut3 | JExplodeArray("col_applyOn", keep = true)                                                         |
|                | ut4 | JExplodeArray("NotExist")                                                                         |
|                | ut5 | JExplodeArray("col_applyOn")                                                                      |