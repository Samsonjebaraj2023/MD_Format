# Driveez DataBase Structure

Here is a detailed overview of Tables and columns in the Driveez database:

### Availability 

The `availability` table is designed to track instructor availability and special day schedules across different branches and schools. It allows for flexible scheduling management with detailed time and status tracking

| Column       | Datatype   |Mandatory	| Description                                                  |
|--------------|:----------:|------|--------------------------------------------------------|
| `ID`         | INT        | Mandatory | Primary key of the table                                     |
| `branch`     | INT        | Mandatory | Indicates the branch                                         |
| `school`     | INT        | Mandatory | Specifies the school                                         |
| `instructor` | INT        | Mandatory | Identifies the instructor                                    |
| `type`       | ENUM       | Mandatory | Regular availability or specialday                           |
| `special_date` | DATE      | Optional | Used for specific date-based availability or special day scheduling |
| `sub`        | INT        | Optional | Potentially used for substitute instructor tracking          |
| `day_of_week`| ENUM       | Mandatory | It specifies the day of a week                               |
| `start_time` | TIME       | Mandatory | Time of availability start                                   |
| `end_time`   | TIME       | Mandatory | Time of availability end                                     |
| `status`     | ENUM       | Mandatory | It specifies Opened or Closed                                |
| `created_at` | DATETIME   | Mandatory | Datetime of record creation                                  |
| `updated_at` | DATETIME   | Optional | Datetime of last update                                      |
| `created_by` | INT        | Mandatory | Identifies the user who created the record                   |
| `updated_by` | INT        | Optional | Identifies the user who last updated the record              |
| `deleted`    | INT        | Optional | Used for soft deletion without removing the record           |


