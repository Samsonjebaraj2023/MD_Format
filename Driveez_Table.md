# Driveez DataBase Structure

Here is a detailed overview of Tables and columns in the Driveez database:

### Availability 

The `availability` table is designed to track instructor availability and special day schedules across different branches and schools. It allows for flexible scheduling management with detailed time and status tracking

| Column       | Datatype   |Mandatory	| Description                                                  |
|--------------|:----------:|:---------:|--------------------------------------------------------|
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
|--------------   |:----------:|:---------: |------------------------------------------------|
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
|--------------   |:----------:|:---------: |------------------------------------------------|
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
|--------------   |:----------:|:---------:|------------------------------------------------|
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
|--------------   |:----------:|:---------:|------------------------------------------------|
| `Id`            | INT        | Yes | Unique identifier for each country record   |
| `code`          | VARCHAR    | Yes | Short country code like `India` > `IND`  |
| `name`          | VARCHAR    | Yes |  Full name of the country   |


### countryprovinces

This table stores detailed information about province within different countries, including their tax-related information and unique identifiers.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `Id`            | INT        | Yes | Unique identifier for each countryprovinces records  |
| `name`          | VARCHAR   | Yes | Full name of the province  |
| `gst`           | DECIMAL    | No  | Goods and Services Tax (GST) rate for the province   |
| `pst`           | DECIMAL     | No  | Provincial Sales Tax (PST) rate   |
| `hst`           | DECIMAL    | No  | Harmonized Sales Tax (HST) rate      |
| `country_code`  | VARCHAR   | Yes | Country code for the province |
| `province_code` | VARCHAR    | Yes | Unique code identifying the province within its country  |

### courses

This table stores comprehensive information about courses offered by schools and branches, including pricing, duration, status, and additional data

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `Id`                | INT        | Yes | Unique identifier for each Course record  |
| `school`            | INT        | Yes | ID of the school offering the course  |
| `branch`            | INT        | Yes | ID of the branch offering the course  |
| `name`              | VARCHAR    | Yes | Full name of the course  |
| `price`             | INT        | Yes |  Course price  |
| `image`             | VARCHAR    | Yes | Path of the course image  |
| `duration`          | DOUBLE     | Yes | Length of the course in hours (theory class + partical class) |
| `period`            | VARCHAR    | Yes | Time period for course duration  |
| `practical_classes` |  DOUBLE    | Yes | Duration of practical classes in hours  |
| `theory_classes`    |  DOUBLE    | Yes | Duration of theory classes in hours  |
| `status`            | ENUM       | Yes | Availability of the course `Available` or `Unavailable` |
| `notes`             | LONGTEXT   | No  | Description about the course |
| `created_at`        | DATETIME   | Yes | Datetime of record creation              |
| `updated_at`        | DATETIME   | No  | Datetime of last update             |
| `deleted`           | TINYINT    | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |
| `created_by`        | INT        | Yes | Identifies the user who created the record      |
| `updated_by`        | INT        | No  | Identifies the user who last updated the record      |
| `imported`          | TINYINT    | No  | Flag indicating if the Course was imported from another source |
| `customX`           | TEXT       | No  | Additional flexible text fields for storing extra course related information   |

### coursesenrolled

This table tracks student course enrollments, including progress, completion status, and associated data across schools and branches.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`                 | INT        | Yes | Unique identifier for each course enrollment record |
| `school`             | INT        | Yes | ID of the school where the course is enrolled|
| `branch`             | INT        | Yes | ID of the branch where the course is enrolled |
| `student`            | INT        | Yes | ID of the student enrolled in the course |
| `course`             | INT        | Yes | ID of the course being enrolled|
| `created_at`         | DATETIME   | Yes | Datetime of record creation |
| `updated_at`         | DATETIME   | Yes | Datetime of last update   |
| `completed_theory`   | DOUBLE     | No  | Completion percentage for theory component |
| `completed_practical`| DOUBLE     | No  | Completion percentage for practical component |
| `completed_on`       | DATE       | No  | Date of course completion |
| `status`             | ENUM       | Yes | Status of course enrollment `Completed` or `Pending` |
| `progress_theory`    | INT        | No  | Progress tracking for theory component |
| `progress_practical` | INT        | No  | Progress tracking for practical component |
| `progress_total`     | INT        | No  | Overall course progress |
| `deleted`            | TINYINT    | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |
| `created_by`         | INT        | Yes | Identifies the user who created the record      |
| `updated_by`         | INT        | No  | Identifies the user who last updated the record    |

### currencies

This table stores comprehensive information about world currencies, providing details for global financial references and transactions.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT        | Yes | Unique identifier for each Currencies record |
| `name`          | VARCHAR    | Yes | Full name of the currency  |
| `code`          | VARCHAR    | Yes | International currency code  |
| `symbol`        | VARCHAR    | Yes | Currency symbol  |

### dataimports

This table is designed to track data import processes, logging details about Excel file imports, their status, and any associated errors

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT     | Yes | Unique identifier for each data import record |
| `imported_by`   | INT     | No  | User ID of the person who initiated the import  |
| `status`        | VARCHAR | No  | Current status of the import process |
| `excel_filename`| VARCHAR | No  | Name of the imported Excel file |
| `excel_filesize`| BIGINT  | No  | Size of the imported Excel file |
| `error_count`   | INT     | No  | Number of errors encountered during import |
| `error_log`     | LONGTEXT| No  | Detailed log of errors that occurred during import |
| `importlog_url` | VARCHAR | No  | URL or path to the detailed import log |

### fleet

This table is for managing vehicles in an training for a driving school 

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT     | Yes | Unique identifier for each fleet vehicle entry |
| `carno_`        | VARCHAR | Yes | car number |
| `carplate`      | VARCHAR | Yes | Vehicle's license plate number |
| `make`          | VARCHAR | Yes | Vehicle manufacturer (e.g., Toyota, Ford) |
| `model`         | VARCHAR | Yes | Specific vehicle model |
| `modelyear`     | VARCHAR | Yes | Year of the vehicle model |
| `school`        | INT     | Yes | Associates the vehicle with a specific school |
| `branch`        | INT     | Yes | Associates the vehicle with a specific branch |
| `instructor`    | INT     | No  | Links the vehicle to a specific instructor |
| `created_at`    | DATETIME| Yes | Datetime of record creation              |
| `updated_at`    | DATETIME| No  | Datetime of last update             |
| `deleted`       | TINYINT | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |
| `created_by`    | INT     | Yes | Identifies the user who created the record      |
| `updated_by`    | INT     | No  | Identifies the user who last updated the record      |
| `imported`      | TINYINT | No  | Flag indicating if the Course was imported from another source |
| `customX`       | TEXT    | No  | Additional flexible text fields for storing extra fleet related information   |

### invoices

This table is designed to manage financial transactions and  tracking detailed invoice information.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT     | Yes | Unique identifier for each Invoice records |
| `reference`     | INT     | Yes | Reference number for the invoice |
| `school`        | INT     | Yes | Associates invoice with a specific school |
| `branch`        | INT     | Yes | Associates invoice with a specific branch |
| `student`       | INT     | Yes | Identifies the student for the invoice |
| `course`        | INT     | Yes | Links invoice to a specific course |
| `product`       | INT     | Yes | Links invoice to a specific product |
| `amount`        | DECIMAL | Yes | Total invoice amount |
| `item`          | TEXT    | Yes | Describes the invoiced items |
| `amountpaid`    | DECIMAL | Yes | Amount paid |
| `raw_cost`      | DECIMAL | No  | Raw cost for paticular course/product |
| `tax_cost`      | DECIMAL | No  | Tax cost for paticular course/product |
| `payment`       | INT     | No  | links to payments table |
| `created_at`    | DATETIME| Yes | Datetime of record creation              |
| `updated_at`    | DATETIME| No  | Datetime of last update             |
| `deleted`       | TINYINT | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |
| `created_by`    | INT     | Yes | Identifies the user who created the record      |
| `updated_by`    | INT     | No  | Identifies the user who last updated the record      |

### languages

This table is store a complete list of world languages with their unique identifiers and standardized codes

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT     | Yes | Unique identifier for each Language records |
| `code`          | INT     | Yes | Code for the language (e.g., en, fr, es) |
| `name`          | VARCHAR | Yes | Full name of the language |

### mail_queue

This table is will manage and track email sending processes and tracking email communications

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT     | Yes | Unique identifier for each email queue entry |
| `to_email`      |VARCHAR  | Yes | Recipient's email address |
| `to_name`       | VARCHAR | Yes | Recipient's name |
| `subject`       |VARCHAR  | Yes | Email subject line|
| `message`       | LONGTEXT| Yes | Full email message content |
| `styles`        | LONGTEXT| No  | styling information for HTML emails |
| `view_data`     | VARCHAR | No  | Reference to a view template  |
| `attachments`   |LONGTEXT | No  | Stores information about email attachments |
| `status`        |ENUM     | Yes | Tracks the current state of the email in the queue `Send` `Failed` `Queued` `Sending` |
| `created_at`    | DATETIME| Yes | Datetime of record creation              |
| `updated_at`    | DATETIME| No  | Datetime of last update             |

### master

This Table stores a Vehical Type , Language and Location information

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT     | Yes | Unique identifier for each master record |
| `code`            | VARCHAR   | Yes | Stores a  code for Vehicle `VT` , Language `LN`, Location Serviced `SU` |
| `data`            | VARCHAR   | Yes | Name of the Paticular data |
| `country_code`            | VARCHAR | Yes |Stores a country code |
| `country_id`            | INT     | Yes | Stores a country ID |

# notifications

This table is to manage a about detailed  notification system information

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT     | Yes | Unique identifier for each notification |
| `user`          | INT     | Yes | Identifies the recipient of the notification |
| `school`        | INT     | Yes | Associates the notification with a specific school |
| `branch`        | INT     | Yes | Associates the notification with a specific branch |
| `type`          | ENUM    | Yes | notification type `newaccount` `payment` `delete` `message` `calender` |
| `class`         | ENUM    | Yes | Class Type `personal` `school` `branch` `system` |
| `message`       | TEXT    | Yes | Contains the actual notification content|
| `created_at`    | DATETIME| Yes | Datetime of record creation              |
| `read`          | BIT     | No  |Tracks whether the notification has been read 0 `Unread` 1 `Read` |
