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

### notifications

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

### payfasttransaction

This table is will track payment transactions, specifically for PayFast payment gateway integrations

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`              | INT     | Yes | Unique identifier for each transaction |
| `m_payment_id`    | INT     | Yes | Unique identifier for each notification |
| `pf_payment_id`   | INT     | Yes | PayFast-specific payment identifier |
| `payment_status`  |VARCHAR  | Yes | Tracks the current status of the payment |
| `item_name`       | LONGTEXT| Yes | Name of the purchased item |
| `item_description`| LONGTEXT| No  | Detailed description of the purchased item |
| `amount_gross`    | DOUBLE  | Yes | Total transaction amount before fees |
| `amount_fee`      | DOUBLE  | Yes | Transaction processing fees |
| `amount_net`      | DOUBLE  | Yes | Net amount after deducting fees |
| `custom_strX`     | VARCHAR | No  | Allows for additional string-based metadata |
| `custom_intX`     | INT     | No  | Allows for additional integer-based metadata|
| `name_first`      | VARCHAR | Yes | Student's first name |
| `name_last`       | VARCHAR | Yes | Student's last name |
| `email_address`   |VARCHAR  | Yes | Student's E-mail address  |
| `merchant_id`     | VARCHAR | Yes | Merchant identification|
| `signature`       | LONGTEXT| Yes | Transaction signature for verification |
| `created_at`      | DATETIME| Yes | Datetime of record creation              |
| `updated_at`      | DATETIME| No  | Datetime of last update             |
| `deleted`         | BIT     | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |
| `created_by`      | INT     | No  | Identifies the user who created the record      |
| `updated_by`      | INT     | No  | Identifies the user who last updated the record      |

### payments

This table tracks transactions across various payment processors, capturing detailed payment information for different types of transactions within the system

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`              | INT     | Yes | Unique identifier for each payment record |
| `transaction_id`  | VARCHAR | Yes |  Unique identifier for the transaction from the payment processor |
| `processor`       | ENUM    | Yes | Payment processor used for the transaction (`PayFast`, `Stripe`, `PayPal`, etc.) |
| `status`          | ENUM    | Yes | Status of the payment transaction (`STARTED` `COMPLETED` `FAILED` `INPROCESS` ) |
| `user`            | INT     | Yes | User associated with the payment |
| `payment_type`    | ENUM    | Yes | Type of payment being processed (`STUDENT_ACTIVATION` `COURSE_FEE` `PRODUCT_FEE`) |
| `amount`          | DECIMAL | Yes | Total amount of the transaction |
| `currency`        | VARCHAR | Yes | Currency of the transaction |
| `invoice`         | INT     | No  | Associated invoice for the payment |
| `course`          | INT     | No  | Associated course for the payment |
| `client_secret`   | VARCHAR | No  | Client authentication |
| `product`         | INT     | No  | Reference to the associated product |
| `raw_cost`        | DECIMAL | No  | Base cost before taxes |
| `tax_cost`        | DECIMAL | No  | Tax amount associated with the transaction |
| `created_at`      |TIMESTAMP| Yes | Datetime of record creation              |
| `updated_at`      | DATETIME| No  | Datetime of last update             |
| `created_by`      | INT     | No  | Identifies the user who created the record      |
| `updated_by`      | INT     | No  | Identifies the user who last updated the record      |
| `deleted`         | TINYINT | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |

### products 

This table is Used to manage a comprehensive product catalog with detailed information and tracking capabilities.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`                 | INT     | Yes | Unique identifier for each product |
| `product_type`       | VARCHAR | Yes | Categorizes the type of product `Digital` `Physical` |
| `product_name`       |  VARCHAR| Yes | Stores the name of the product|
| `product_description`| LONGTEXT| Yes | Provides a detailed description of the product |
| `price`              | INT     | Yes | Stores the product price |
| `thumbnail`          | VARCHAR | Yes | URL to the product's thumbnail image |
| `url`                | VARCHAR | No  | stores a link to the product page or additional information |
| `status`             | VARCHAR | YeS | Tracks the current status of the product |
| `created_by`         | INT     | No  | Identifies the user who created the record      |
| `updated_by`         | INT     | No  | Identifies the user who last updated the record      |
| `created_on`         | DATETIME| No  | Datetime of record creation              |
| `updated_on`         | DATETIME| Yes | Datetime of last update             |

### product_enrolled

This table tracks student enrollments in products across different schools and branches, capturing detailed information about product registration and administrative metadata

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`                 | INT     | Yes | Unique identifier for each product enrollment record |
| `school`             | INT     | Yes | School associated with the product enrollment |
| `branch`             | INT     | Yes | Branch associated with the product enrollment |
| `student`            | INT     | Yes | Student  enrolled in the product |
| `product`            | INT     | Yes | Product being enrolled in |
| `created_by`         | INT     | Yes | User ID of the record creator     |
| `updated_by`         | INT     | Yes | User ID of the last record updater      |
| `created_on`         | DATETIME| Yes | Datetime of record creation              |
| `updated_on`         | DATETIME| Yes | Datetime of last update             |

### pushnotification_queue

This table manages a queue of push notifications, tracking their status, content, and delivery progress across the system.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT      | Yes | Unique identifier for each push notification queue records |
| `token`         |LONGTEXT  | Yes | user token for push notification delivery |
| `title`         | LONGTEXT | Yes | Title of the push notification |
| `body`          | LONGTEXT | Yes | Content body of the push notification |
| `created_at`    |TIMESTAMP |Yes  | Datetime of record creation              |
| `updated_at`    | TIMESTAMP| Yes | Datetime of last update             |
| `status`        | ENUM     | Yes | Current status of the push notification `Send` `Failed` `Queued` `Sending` |

### reminders

This table manages reminder configurations for different schools, defining systematic notifications for classes and payments via email or SMS

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT      | Yes | Unique identifier for each reminder configuration |
| `school`        | INT      | Yes | School associated with the reminder configuration |
| `subject`       |VARCHAR   | Yes |  Subject of the reminder |
| `days`          | INT      | Yes | Number of days relative to the due date for sending the reminder |
| `message`       | TEXT     | Yes | Detailed message content for the reminder |
| `type`          | ENUM     | Yes | Type of reminder being configured `class` `Payment` |
| `send_via`      | ENUM     | Yes | Communication channel for sending reminders `SMS` `Email` |
| `id`            | ENUM     | Yes |  Timing of reminder relative to the due date `before_due` `after_due` |

### reports

This table stores predefined report configurations, including query details, filters, and metadata for generating dynamic system reports across various domains.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT      | Yes | Unique identifier for each report configuration |
| `label`         | VARCHAR  | Yes |  Title of the report |
| `key`           | VARCHAR  | Yes | Unique system identifier for the report |
| `query`         | LONGTEXT | Yes |  Database query used to generate the report |
| `status`        | VARCHAR  | Yes |  Current status of the report configuration |
| `filters`       | LONGTEXT | Yes | structured data defining report filter configurations (`date` , `course` , `student` .. )|
| `description`   |LONGTEXT  | Yes | Detailed explanation of the report's purpose and contents |

### schoolmessages

This table tracks communication messages sent within the school system, capturing details of SMS and email communications across schools and branches.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`            | INT      | Yes | Unique identifier for each school message record |
| `receiver`      | INT      | Yes | Identifier of the message receiver |
| `type`          | ENUM     | Yes | Communication channel for sending reminders `SMS` `Email` |
| `contact`       |VARCHAR   | Yes | Contact information|
| `subject`       | VARCHAR  | Yes |  Message subject  |
| `message`       | LONGTEXT | Yes | Full message content |
| `sent_at`       | TIMESTAMP| Yes | Timestamp when the message was sent |
| `status`        | ENUM     | Yes | Delivery status of the message `Sent` `Failed` |
| `school`        | INT      | Yes | Unique identifier for each report configuration |
| `branch`        | INT      | Yes | Unique identifier for each report configuration |

### schools

 Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`                      | INT     | Yes | Unique identifier for each school record |
| `name`                    | VARCHAR | Yes | School name |
| `email`                   | VARCHAR | Yes | School contact email |
| `phone`                   | VARCHAR | Yes | School contact phone number |
| `address`                 | VARCHAR | Yes | School physical address |
| `currency`                | VARCHAR | Yes | Specifies the default currency for the school |
| `timezone`                | VARCHAR | Yes |  Sets the default timezone for the school |
| `payment_reminders`       | ENUM    | Yes | Payment reminder settings `on` `off` |
| `status`                  | ENUM    | Yes | Current operational status of the school `Active` `Suspended` |
| `class_reminders`         | ENUM    | Yes | Class reminder settings `on` `off` |
| `created_at`              | DATETIME| Yes | Automatically records when the school record was created |
| `country_code`            | VARCHAR | Yes | School's country identifier |
| `language_code`           | VARCHAR | Yes | School's language setting |
| `paid_activation`         | TINYINT | Yes | If its on then (`1`) student will pay the activation fee or else it will be `0` |
| `paid_activation_fees`    | DECIMAL | Yes | Activation fees for student  |
| `paid_enrollment`         | TINYINT | Yes | Paid Enrollement is on > `1` off >  `0` |
| `allow_edit_pickup`       | INT     | Yes | School allows edit pickup on > `1` Off > `0` |
| `payfast_merchant_id`     | VARCHAR | Yes | Payfast Merchant ID for the school |
| `payfast_merchant_key`    | VARCHAR | Yes | Payfast Merchant Key for the school |
| `payfast_passphrase`      | VARCHAR | Yes | Payfast Passphrase for the school |
| `payfast_environment`     | VARCHAR | Yes | Payfast Environment `sandbox` `live` |
| `province_code`           | VARCHAR | Yes  | Provinces code for a School   |
| `allowed_inactive_days`   | INT     | Yes  | How many days student can inactive  |
| `sms_enabled`             | INT     | Yes  | SMS will be  on > `1` Off > `0`   |
| `paystack_public_key`     | VARCHAR | Yes  | Paystack Public Key for the school |
| `paystack_secret_key`     | VARCHAR | Yes | Paystack Secret Key for the school |
| `stripe_public_key`       | VARCHAR | Yes | Stripe Public Key for the school |
| `stripe_secret_key`       | VARCHAR | Yes | Stripe Secret Key for the school |
| `paypal_client_id`        | VARCHAR | Yes | Paypal Client ID for the school |
| `paypal_secret_key`       | VARCHAR | Yes | Paypal Secret Key for the school |
| `chat_enabled`            | INT     | Yes | Chat will be  on > `1` Off > `0`   |
| `whatsapp_enabled`        | INT     | Yes |  WhatsApp will be  on > `1` Off > `0`   |
| `whatsapp_username`       | VARCHAR | Yes | Whatsapp username for the school |
| `whatsapp_password`       | VARCHAR | Yes | Whatsapp password for the school |
| `signup_url`              | VARCHAR | Yes | For Student or Instructor sign up URl |
| `signin_url`              | VARCHAR | Yes | For Student or Instructor sign in URl |
| `notify_url`              | VARCHAR | Yes | For Student or Instructor notify URl |
| `cash`                    | ENUM    | Yes | If its on then (`1`) student will pay the cash or else it will be `0` |
| `bank_transfer`           | ENUM    | Yes | If its on then (`1`) student can bank transfer or else it will be `0` |
| `payment_gateway`         | ENUM    | Yes | If its on then (`1`) student will pay the payment gateway or else it will be `0` |
| `stripe_gateway`          | ENUM    | Yes | `1` Enable Stripe Gateway `0` Disable Stripe Gateway |
| `paystack_gateway`        | ENUM    | Yes | `1` Enable Paystack Gateway `0` Disable Paystack Gateway |
| `payfast_gateway`         | ENUM    | Yes | `1` Enable Payfast Gateway `0` Disable Payfast Gateway |
| `paypal_gateway`          | ENUM    | Yes | `1` Enable PayPal Gateway `0` Disable PayPal Gateway |
| `paynow_gateway`          | ENUM    | Yes | `1` Enable Paynow Gateway `0` Disable Paynow Gateway |
| `cash_instruction`        | VARCHAR | Yes | Description of Cash payment  |
| `banktransfer_instruction`| VARCHAR | Yes | Description of Bank Transfer payment  |
| `product_tour_enabled`    | INT     | Yes | `1` Enable Product Tour `0` Disable Product Tour |
| `marketplace_enabled`     | INT     | Yes | `1` Enable Marketplace `0` Disable Marketplace |
| `paynow_integration_id`   | VARCHAR | Yes | Paynow Integration ID for the school |
| `paynow_integration_key`  | VARCHAR | Yes | Paynow Integration Key for the school |
| `paynow_test_email`       | VARCHAR | Yes | Paynow Test Email for the school |


### sessioninstructor

This Table Manages the relationship between sessions and instructors

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`              | INT     | Yes | Unique identifier for each session-instructor assignment |
| `session`         | INT     | Yes | Indicates which session the instructor is assigned to |
| `instructor`      | INT     | Yes | Represents the instructor assigned to the session |
| `created_at`      |TIMESTAMP| Yes | Datetime of record creation              |
| `updated_at`      | DATETIME| No  | Datetime of last update             |
| `created_by`      | INT     | Yes | Identifies the user who created the record      |
| `updated_by`      | INT     | Yes | Identifies the user who last updated the record      |
| `deleted`         | TINYINT | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |

### sessions

This Table to track and organize sessions across different contexts

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`          | INT     | Yes | Unique identifier for each session |
| `school`      | INT     | Yes | References the school hosting the session |
| `branch`      | INT     | Yes | References the specific branch where the session occurs |
| `start_date`  | DATE    | Yes | Indicates the Start day of the session |
| `end_date`    | DATE    | Yes |Indicates the End day of the session |
| `course`      | INT     | No  | reference to the associated course |
| `class_type`  | ENUM    | Yes | `Partical` or `Theory` |
| `map_url`     | LONGTEXT | No  | reference to geographical location |
| `location`    | LONGTEXT| Yes | Detailed location description |
| `name`        | VARCHAR  | Yes |  Title for the session |
| `session_type`| ENUM    | No  | `in-person`, `group` |
| `days`        | LONGTEXT| Yes | Specific days of session occurrence |
| `duration`    | INT     | Yes | Length of the session in minutes |
| `start_time`  | VARCHAR | Yes | Specifies the session's start time |
| `occurence`   | ENUM    | Yes | Defines the session's recurrence pattern  `allweekday`, `weekend`, `specific`|
| `status`      | ENUM    | Yes | `new`, `inprogress`, `completed` |
| `created_at`  |TIMESTAMP| Yes | Datetime of record creation              |
| `updated_at`  | DATETIME| No  | Datetime of last update             |
| `created_by`  | INT     | Yes | Identifies the user who created the record      |
| `updated_by`  | INT     | Yes | Identifies the user who last updated the record      |
| `deleted`     | TINYINT | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |


### slotenrolled

This table stored student enrollment in specific session slots, providing detailed tracking of student participation and progress

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`          | INT     | Yes | Unique identifier for each enrollment record |
| `session`     | INT     | Yes | References the specific session |
| `student`     | INT     | Yes | References the student enrolled in the slot |
| `slot`        | INT     | Yes | Identifies the specific slot within the session|
| `completed`   | TINYINT | Yes | Tracks whether the student has completed the slot |
| `created_at`  |DATETIME | Yes | Datetime of record creation              |
| `updated_at`  | DATETIME| No  | Datetime of last update             |
| `created_by`  | INT     | Yes | Identifies the user who created the record      |
| `updated_by`  | INT     | Yes | Identifies the user who last updated the record      |
| `deleted`     | TINYINT | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |

### slotnotes

This Table support complex communication scenarios with multiple recipients and detailed tracking.

| Column          | Datatype   |Mandatory	| Description                                    |
|--------------   |:----------:|:---------:|------------------------------------------------|
| `id`           | INT       | Yes | Unique identifier for each note |
| `note_to`      | VARCHAR   | No  | text-based recipient identifier |
| `content`      | MEDIUMTEXT| Yes | Main body of the note |
| `note_from`    | INT       | Yes | Unique identifier for each enrollment record |
| `note_to_X`    | INT       | Yes | Allows up to 10 simultaneous recipients |
| `sent`         | INT       | Yes | Tracks sending status  |
| `signature_url`| VARCHAR   | No  | URL for digital signature |
| `slot_id`      | INT       | Yes | Provides contextual information |
| `created_at`   |DATETIME   | Yes | Datetime of record creation              |
| `updated_at`   | DATETIME  | No  | Datetime of last update             |
| `created_by`   | INT       | Yes | Identifies the user who created the record      |
| `updated_by`   | INT       | Yes | Identifies the user who last updated the record      |
| `removed`      | TINYINT   | No  | Soft delete flag (`0` = not deleted, `1` = deleted)     |

