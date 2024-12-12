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
| `deleted`    | TINYINT    | No | Soft delete flag (`0` = not deleted, `1` = deleted)           |


### branchattachments

This Table to store attachments associated with branches, tracking document uploads, their metadata, and related user information.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|----------- |------------------------------------------------|
| `ID`            | INT        | Yes | Primary key of the table          |
| `uploaded_by`   | INT        | Yes | ID of the user who uploaded |
| `attachment_for`| INT        | Yes | ID of the branch to which the attachment is linked   |
| `attachment`    | VARCHAR    | Yes | path of the uploaded attachment in S3             |
| `name`          | VARCHAR    | Yes | Display name of the attachment    |
| `type`          | ENUM       | Yes | Type of attachment (currently limited to 'document')      |
| `created_at`    | DATETIME   | Yes | Datetime of record creation              |
| `updated_at`    | DATETIME   | No  | Datetime of last update             |
| `deleted`       | TINYINT    | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |
| `created_by`    | INT        | Yes | Identifies the user who created the record      |
| `updated_by`    | INT        | No  | Identifies the user who last updated the record      |

### branches

This table stores information about different branches, including their contact details, associated school, status, and additional custom fields.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|----------- |------------------------------------------------|
| `ID`            | INT        | Yes | Primary key of the table          |
| `name`          | VARCHAR    | Yes | Name of the branch      |
| `school`        | INT        | Yes | ID of the school to which the branch belongs    |
| `email`         | VARCHAR    | Yes | Contact email address of the branch        |
| `address`       | VARCHAR    | Yes | Physical address of the branch        |
| `postalcode`    | INT        | No  | Postal code of the branch location  |
| `phone`         | VARCHAR    | Yes | Contact phone number of the branch   |
| `type`          | ENUM       | No  | `Headquarters` or `branch`   |
| `map_location`  | VARCHAR    | No  | location or map coordinates of the branch |
| `tax_number`    | INT        | No  | Tax identification number of the branch     |
| `status`        | ENUM       | Yes | `Active` or `inactive`     |
| `created_at`    | DATETIME   | Yes | Datetime of record creation              |
| `updated_at`    | DATETIME   | No  | Datetime of last update             |
| `deleted`       | TINYINT    | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |
| `created_by`    | INT        | Yes | Identifies the user who created the record      |
| `updated_by`    | INT        | No  | Identifies the user who last updated the record      |
| `imported`      | TINYINT    | No  | Flag indicating if the branch was imported from another source |
| `customX`       | TEXT       | No  | Additional flexible text fields for storing extra branch-related information   |

### branchmessages

This table tracks messages sent to branches, including communication details and delivery status

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|----------- |------------------------------------------------|
| `status`        | ENUM       | Yes | Current delivery status of the message `Sent` or `Failed` or `Queued` or`Sending`     |
| `id`            | INT        | Yes | Primary key of the table          |
| `receiver`      | INT        | Yes | ID of the branch receiving the message     |
| `type`          | ENUM       | Yes | Communication channel type `sms` or `email`        |
| `contact`       | VARCHAR    | Yes |  Contact information (phone number or email address)        |
| `subject`       | VARCHAR    | No  |  Message subject or title       |
| `message`       | LONGTEXT   | No  | Full text content of the message   |
| `sent_at`       | TIMESTAMP  | Yes | Timestamp when the message was sent/queued |
| `school`        | INT        | Yes | ID of the school associated with the message   |
| `branch`        | INT        | Yes | ID of the specific branch associated with the message   |
| `view_type`     |VARCHAR     | No  | Additional classification or view type for the message  |

### countries

This table stores information about different countries, providing a comprehensive list with unique identifiers, country codes, and names.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|----------- |------------------------------------------------|
| `ID`            | INT        | Yes | Unique identifier for each country record   |
| `code`          | VARCHAR    | Yes | Short country code like `India` > `IND`  |
| `name`          | VARCHAR    | Yes |  Full name of the country   |
