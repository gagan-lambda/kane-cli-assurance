---
assurance:
  id: t-6
  base: sha256:44587d3d57f7eed4cf946cc1180f88050967c853dd4c45008b53698d51157631
---
# Reject a too-early Start Date and keep Optional Products independent

> Prove Step 3 rejects a too-early Start Date with a clear message and that Optional Products can be selected and deselected independently without coupling.

## Step 1

Open https://sampleapp.tricentis.com/101/index.php in a fresh browser session.

## Step 2

On the landing page, select the Automobile category and complete Step 1 with Make Audi, Engine Performance (kW) 110, Date of Manufacture {{valid_manufacture_date}}, Number of Seats 5, Fuel Type Petrol, List Price 30000, and Annual Mileage 10000 to reach Step 2.

## Step 3

On Step 2 'Enter Insurant Data', enter First Name {{valid_first_name}}, Last Name {{valid_last_name}}, Date of Birth {{insurable_birth_date}}, select Male, Street Address {{valid_street_address}}, Country Germany, Zip Code {{valid_zip_code}}, City {{valid_city}}, Occupation Employee, select the Speeding hobby, leave Picture upload empty, and continue to Step 3.

## Step 4 @verifies ac-17, ac-18

On Step 3 'Enter Product Data', inspect the available Damage Insurance and Courtesy Car choices, then assert the Damage Insurance options are exactly No coverage, Partial coverage, and Full coverage, and the Courtesy Car options are exactly Yes and No.

## Step 5 @verifies ac-15

On Step 3, set Start Date to {{too_early_start_date}}, choose Insurance Sum {{valid_insurance_sum}}, Merit Rating {{valid_merit_rating}}, Damage Insurance Partial coverage, leave Optional Products unselected, choose Courtesy Car No, and try to continue, then assert a clear Start Date validation message is shown and Step 4 is not displayed.

## Step 6 @verifies ac-16

Still on Step 3 after restoring Start Date to a date 90 days after the run date, select Euro Protection only and assert Legal Defense Insurance remains unselected; then select Legal Defense Insurance as well and assert both options are selected; then clear Euro Protection and assert Legal Defense Insurance remains selected.
