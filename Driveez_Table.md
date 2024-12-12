# Driveez DataBase Structure

Here is a detailed overview of Tables and columns in the Driveez database:

### Availability 

The `availability` table is designed to track instructor availability and special day schedules across different branches and schools. It allows for flexible scheduling management with detailed time and status tracking

| Column       | Datatype   | Description                                                  |
|--------------|:----------:|--------------------------------------------------------------|
| `ID`         | INT        | Primary key of the table                                     |
| `branch`     | INT        | Indicates the branch                                         |
| `school`     | INT        | Specifies the school                                         |
| `instructor` | INT        | Identifies the instructor                                    |
| `type`       | ENUM       | Regular availability or specialday                           |
| `special_date` | DATE      | Used for specific date-based availability or special day scheduling |
| `sub`        | INT        | Potentially used for substitute instructor tracking          |
| `day_of_week`| ENUM       | It specifies the day of a week                               |
| `start_time` | TIME       | Time of availability start                                   |
| `end_time`   | TIME       | Time of availability end                                     |
| `status`     | ENUM       | It specifies Opened or Closed                                |
| `created_at` | DATETIME   | Datetime of record creation                                  |
| `updated_at` | DATETIME   | Datetime of last update                                      |
| `created_by` | INT        | Identifies the user who created the record                   |
| `updated_by` | INT        | Identifies the user who last updated the record              |
| `deleted`    | INT        | Used for soft deletion without removing the record           |


