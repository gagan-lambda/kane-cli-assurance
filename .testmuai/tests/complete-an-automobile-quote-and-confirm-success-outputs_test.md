---
assurance:
  id: t-1
  base: sha256:52dd9ff2eecff11b7770f9097166dac36ea4c176edddf28ec7eff887959eeb0a
---
# Complete an Automobile quote and confirm success outputs

> Prove a prospective customer can complete the full five-step Automobile quote journey with valid data, choose one price tier, submit successfully, and receive the promised confirmation outputs.

## Step 1

Open https://sampleapp.tricentis.com/101/index.php in a fresh browser session.

## Step 2 @verifies ac-8

On the landing page, select the Automobile category, then assert Step 1 'Enter Vehicle Data' is displayed.

## Step 3

On Step 1 'Enter Vehicle Data' for Automobile, set Make to Audi, Engine Performance (kW) to 110, Date of Manufacture to {{valid_manufacture_date}}, Number of Seats to 5, Fuel Type to Petrol, List Price to 30000, Annual Mileage to 10000, and continue to Step 2.

## Step 4 @verifies ac-14

On Step 2 'Enter Insurant Data', enter First Name {{valid_first_name}}, Last Name {{valid_last_name}}, Date of Birth {{insurable_birth_date}}, select Male, Street Address {{valid_street_address}}, Country Germany, Zip Code {{valid_zip_code}}, City {{valid_city}}, Occupation Employee, select the Speeding hobby, leave Picture upload empty, and continue to Step 3, then assert Step 3 'Enter Product Data' is displayed without requiring a picture upload.

## Step 5

On Step 3 'Enter Product Data', set Start Date to a date 90 days after the run date, choose Insurance Sum {{valid_insurance_sum}}, Merit Rating {{valid_merit_rating}}, Damage Insurance Full coverage, select both Optional Products, choose Courtesy Car Yes, and continue to Step 4.

## Step 6 @verifies ac-6

On Step 4 'Select Price Option', choose Platinum and continue to Step 5, then assert Platinum is the only selected tier.

## Step 7 @verifies ac-1, ac-2

On Step 5 'Send Quote', enter E-Mail {{valid_email}}, Phone {{valid_phone}}, Username {{valid_username}}, Password {{valid_password}}, Confirm Password {{valid_password}}, leave Comments empty, send the quote, then assert a success confirmation dialog is shown and the browser or captured network exposes /101/tcpdf/pdfs/quote.php for the generated quote PDF.
