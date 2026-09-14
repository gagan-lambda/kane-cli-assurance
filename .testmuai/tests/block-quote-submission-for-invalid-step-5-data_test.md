---
assurance:
  id: t-3
  base: sha256:c4e8d68344a4d024c10f159fc7ce7a9b0a2be8f4c612124136e42646e9e7bd02
---
# Block quote submission for invalid Step 5 data

> Prove Step 5 blocks submission when the e-mail format is malformed and also blocks submission when Password and Confirm Password do not match.

## Step 1

Open https://sampleapp.tricentis.com/101/index.php in a fresh browser session.

## Step 2

On the landing page, select the Automobile category and complete Step 1 with Make Audi, Engine Performance (kW) 110, Date of Manufacture {{valid_manufacture_date}}, Number of Seats 5, Fuel Type Petrol, List Price 30000, and Annual Mileage 10000 to reach Step 2.

## Step 3

On Step 2 'Enter Insurant Data', enter First Name {{valid_first_name}}, Last Name {{valid_last_name}}, Date of Birth {{insurable_birth_date}}, select Male, Street Address {{valid_street_address}}, Country Germany, Zip Code {{valid_zip_code}}, City {{valid_city}}, Occupation Employee, select the Speeding hobby, leave Picture upload empty, and continue to Step 3.

## Step 4

On Step 3 'Enter Product Data', set Start Date to a date 90 days after the run date, choose Insurance Sum {{valid_insurance_sum}}, Merit Rating {{valid_merit_rating}}, Damage Insurance Full coverage, select both Optional Products, choose Courtesy Car Yes, and continue to Step 4.

## Step 5

On Step 4 'Select Price Option', choose Silver and continue to Step 5.

## Step 6 @verifies ac-19

On Step 5 'Send Quote', enter E-Mail {{malformed_email}}, Phone {{valid_phone}}, Username {{valid_username}}, Password {{valid_password}}, Confirm Password {{valid_password}}, and send the quote, then assert no success confirmation dialog is shown and the E-Mail field is visibly invalid.

## Step 7 @verifies ac-20

Still on Step 5, correct E-Mail to {{valid_email}}, enter Password {{valid_password}} and Confirm Password {{mismatched_confirm_password}}, send the quote again, then assert no success confirmation dialog is shown and the password mismatch is visibly indicated.
