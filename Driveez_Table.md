# Driveez DataBase Structure

Here is a detailed overview of Tables and columns in the Driveez database:

### Availability 

The `availability` table is designed to track instructor availability and special day schedules across different branches and schools. It allows for flexible scheduling management with detailed time and status tracking

| Column       | Datatype   |Mandatory	| Description                                                  |
|--------------|:----------:|------|--------------------------------------------------------|
| `ID`         | INT        | Yes | Primary key of the table                                     |
| `branch`     | INT        | Yes | Indicates the branch                                         |
| `school`     | INT        | Yes | Specifies the school                                         |
| `instructor` | INT        | Yes | Identifies the instructor                                    |
| `type`       | ENUM       | Yes | Regular availability or specialday                           |
| `special_date` | DATE      | No | Used for specific date-based availability or special day scheduling |
| `sub`        | INT        | No | Potentially used for substitute instructor tracking          |
| `day_of_week`| ENUM       | Yes | It specifies the day of a week                               |
| `start_time` | TIME       | Yes | Time of availability start                                   |
| `end_time`   | TIME       | Yes | Time of availability end                                     |
| `status`     | ENUM       | Yes | It specifies Opened or Closed                                |
| `created_at` | DATETIME   | Yes | Datetime of record creation                                  |
| `updated_at` | DATETIME   | No | Datetime of last update                                      |
| `created_by` | INT        | Yes | Identifies the user who created the record                   |
| `updated_by` | INT        | No | Identifies the user who last updated the record              |
| `deleted`    | INT        | No | Used for soft deletion without removing the record           |
    
