# Hosting JSONs

- Objective make each of couple input / expected work
  - Each ut contains
    - `input.json` => The input JSON
    - `input_sch.txt` => Do not mind this
    - `expected.json` => The expected JSON & DataFrame view
    - `expected_sch.txt` => The expected DataFrame columns types
  - _If there is no `expected.json` and `expected_sch.txt` the user must be alert that his step is invalid_
- You can directly retrieve it via API using `Raw` feature from GitHub (for example [this](https://raw.githubusercontent.com/jjiadtgy/hosting_jsons/main/JSelectKeyExecuteStepTest/ut1/input.json))
- Table parameters for each unit tests

| JParsingStep   | UT                                                                                       | Parameters                                                                                        |
|----------------|------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| JSelectKey     | **UT1** - Only selecting the root "JSON keys"                                            | JSelectKey(selectedKeysAre = Array("col_nominal_struct", "col_nominal", "col_not.nominal_struct") |
|                | **UT2** - Exception on non-existing columns                                              | JSelectKey(selectedKeysAre = Array("col_non_existing")                                            |
| JSelectStruct  | **UT1** - Nominal case with existing `applyOn` & all existing `selectedKeysAre` key(s)   | JSelectStruct("col_applyOn", selectedKeysAre = Array("sub2", "sub0"))                             |
|                | **UT2** - Works even with `applyOn` and `selectedKeysAre` with accessor character(s) "." | JSelectStruct("col.applyOn", selectedKeysAre = Array("sub.0"))                                    |
|                | **UT3** - Provoke duplicated column names but managed                                    | SelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array("col_duplicated"))                  |
|                | **UT4** - Testing keep `true`                                                            | JSelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array("sub0"), keep = true)              |
|                | **UT5** - Empty `selectedKeysAre`                                                        | JSelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array.empty)                             |
|                | **UT6** - Missing `applyOn` column in the DataFrame causing exception                    | JSelectStruct(applyOn = "NotExist", selectedKeysAre = Array("sub0"))                              |
|                | **UT7** - Missing one of the `selectedKeysAre` key in the DataFrame causing exception    | JSelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array("NotExist"))                       |
|                | **UT8** - `applyOn` not a struct                                                         | JSelectStruct(applyOn = "col_applyOn", selectedKeysAre = Array("sub0"))                           |
| JSelectArray   | **UT1** - Nominal case & Not reachable `index`                                           | JSelectArray("col_applyOn", 1)                                                                    |
|                | **UT2** - Negative index as not reachable `index`                                        | JSelectArray("col_applyOn", -1)                                                                   |
|                | **UT3** - Testing keep `true` for `JSelectArray`                                         | JSelectArray("col_applyOn", 0, keep = true)                                                       |
|                | **UT4** - Missing `applyOn` column in the DataFrame causing exception                    | JSelectArray("NotExist", 0)                                                                       |
|                | **UT5** - `applyOn` not an array                                                         | JSelectArray("col_applyOn", 0)                                                                    |
| JExplodeStruct | **UT1** - Nominal case with existing `applyOn`                                           | JExplodeStruct("col_applyOn")                                                                     |
|                | **UT2** - Works even with `applyOn` and sub-columns with accessor character(s) "."       | JExplodeStruct("col.applyOn")                                                                     |
|                | **UT3** - Provoke duplicated column names but managed (JExplodeStruct)                   | JExplodeStruct("col_applyOn")                                                                     |
|                | **UT4** - Testing keep `true` for `JExplodeStruct`                                       | JExplodeStruct("col_applyOn", keep = true)                                                        |
|                | **UT5** - Empty sub-columns                                                              | JExplodeStruct("col_applyOn")                                                                     |
|                | **UT6** - Missing `applyOn` column in the DataFrame causing exception (JExplodeStruct)   | JExplodeStruct("NotExist")                                                                        |
|                | **UT7** - `applyOn` not a struct (JExplodeStruct)                                        | JExplodeStruct("col_applyOn")                                                                     |
| JExplodeArray  | **UT1** - Nominal case with any elements & multiple rows                                 | JExplodeArray("col_applyOn")                                                                      |
|                | **UT2** - `applyOn` is `null`                                                            | JExplodeArray("col_applyOn")                                                                      |
|                | **UT3** - Testing keep `true` for `JExplodeArray`                                        | JExplodeArray("col_applyOn", keep = true)                                                         |
|                | **UT4** - Missing `applyOn` column in the DataFrame causing exception                    | JExplodeArray("NotExist")                                                                         |
|                | **UT5** - `applyOn` not an array                                                         | JExplodeArray("col_applyOn")                                                                      |