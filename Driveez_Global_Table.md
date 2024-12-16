# Driveez Global DataBase Structure

Here is a detailed overview of Driveez global database:

### tenants

The table used to manage multi-tenant configuration details for a software platform, storing critical information about different organizational instances or clients within a single system

| Column       | Datatype   |Mandatory	| Description                                                  |
|--------------|:----------:|:---------:|--------------------------------------------------------|
| `ID`                | INT        | Yes | Unique identifier for each tenants  |
| `title`             | VARCHAR | No  | Tenant's organization name |
| `legal_entity`      | VARCHAR | No  |  Legal name of the organization |
| `subdomain`         | VARCHAR | No  | Unique subdomain for the tenant's platform access |
| `plan`              | VARCHAR | No  | Subscription or service plan type|
| `db_host`           | VARCHAR | No  | Database host address |
| `db_name`           | VARCHAR | No  | Database name |
| `db_user`           | VARCHAR | No  | Database user |
| `db_pass`           | VARCHAR | No  | Database password |
| `logo_url`          | VARCHAR | No  | URL for the tenant's logo |
| `favicon_url`       | VARCHAR | No  | URL for the tenant's favicon |
| `db_port`           | INT     | No  | Database connection port |
| `payment_gateway`   | ENUM    | No  | Payment gateway used by the tenant `Stripe` `PayPal` `Payfast` `Paystack` `Paynow` |
| `stripe_pkey`       | VARCHAR | No  | Stripe public key of tenant |
| `stripe_skey`       | VARCHAR | No  | Stripe secret key of tenant |
| `ency_stripe_pkey`  | VARCHAR | No  | Stripe public key of ency |
| `ency_stripe_skey`  | VARCHAR | No  | Stripe secret key of ency |
| `stripe_methods`    | VARCHAR | No  | Supported Stripe payment methods|
| `db_passhash`       | VARCHAR | No  | Hashed database password for additional security |
| `api_jwtsecret`     | VARCHAR | No  | JWT (JSON Web Token) secret for API authentication |
| `student_sign_up`   | TINYINT | No  | If its `1` then student can sign up otherwise not |