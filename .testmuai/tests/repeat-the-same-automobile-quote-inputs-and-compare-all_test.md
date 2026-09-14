---
assurance:
  id: t-2
  base: sha256:9f74f179c3876c4446b821e7b6b1192c93f43dee074a9c757e0f7b1ceb47816f
---
# Repeat the same Automobile quote inputs and compare all price tiers

> Prove that identical same-day inputs produce stable price displays across repeated runs, that the tier prices remain ordered from Silver through Ultimate, and that only one tier is selected at a time when a choice is made.

## Step 1

Open https://sampleapp.tricentis.com/101/index.php in a fresh browser session.

## Step 2

On the landing page, select the Automobile category and complete Step 1 with Make Audi, Engine Performance (kW) 110, Date of Manufacture {{valid_manufacture_date}}, Number of Seats 5, Fuel Type Petrol, List Price 30000, and Annual Mileage 10000 to reach Step 2.

## Step 3

On Step 2 'Enter Insurant Data', enter First Name {{valid_first_name}}, Last Name {{valid_last_name}}, Date of Birth {{insurable_birth_date}}, select Male, Street Address {{valid_street_address}}, Country Germany, Zip Code {{valid_zip_code}}, City {{valid_city}}, Occupation Employee, select the Speeding hobby, leave Picture upload empty, and continue to Step 3.

## Step 4

On Step 3 'Enter Product Data', set Start Date to a date 90 days after the run date, choose Insurance Sum {{valid_insurance_sum}}, Merit Rating {{valid_merit_rating}}, Damage Insurance Full coverage, select both Optional Products, choose Courtesy Car Yes, and continue to Step 4.

## Step 5 @verifies ac-6

On the first Step 4 'Select Price Option' visit, store the displayed Silver, Gold, Platinum, and Ultimate prices as first_run_silver, first_run_gold, first_run_platinum, and first_run_ultimate, choose Gold, and continue only after asserting Gold is the only selected tier.

## Step 6

Return to https://sampleapp.tricentis.com/101/index.php in the same browser session and repeat the same Automobile, insurant, and product inputs through Step 4.

## Step 7 @verifies ac-4, ac-5

On the second Step 4 'Select Price Option' visit, compare the displayed Silver, Gold, Platinum, and Ultimate prices with first_run_silver, first_run_gold, first_run_platinum, and first_run_ultimate, then assert all four prices exactly match the first run and the displayed order is Silver < Gold < Platinum < Ultimate.
