---
assurance:
  id: t-5
  base: sha256:23fb1bfcbe5f4a5543bd93c5ef33b6c1bce75b75dad32e77526f5b710a86ff89
---
# Block Step 1 progression for empty required fields and invalid numeric input

> Prove Step 1 blocks progression both when mandatory fields are empty and when a numeric field contains non-numeric input.

## Step 1

Open https://sampleapp.tricentis.com/101/index.php in a fresh browser session.

## Step 2 @verifies ac-8

On the landing page, select Automobile, then assert Step 1 'Enter Vehicle Data' is displayed.

## Step 3 @verifies ac-9

On Step 1 with all fields left empty, choose Next, then assert Step 2 is not displayed and the mandatory Step 1 fields are visibly flagged.

## Step 4 @verifies ac-10, ac-24

Still on Step 1, set Make to Audi, Engine Performance (kW) to {{invalid_numeric_text}}, Date of Manufacture to {{valid_manufacture_date}}, Number of Seats to 5, Fuel Type to Petrol, List Price to 30000, Annual Mileage to 10000, and choose Next, then assert Step 2 is still not displayed and the numeric field is rejected or visibly marked invalid.
