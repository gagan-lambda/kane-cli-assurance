---
assurance:
  id: t-8
  base: sha256:62ebdd8b8a58ac9480e1570c25345609999518d5d1516a7b61818155d4539fa9
---
# Reject a future Date of Birth and keep gender single-choice

> Prove Step 2 rejects a non-past Date of Birth while the gender control remains mutually exclusive when the user changes selection.

## Step 1

Open https://sampleapp.tricentis.com/101/index.php in a fresh browser session.

## Step 2

On the landing page, select the Automobile category and complete Step 1 with Make Audi, Engine Performance (kW) 110, Date of Manufacture {{valid_manufacture_date}}, Number of Seats 5, Fuel Type Petrol, List Price 30000, and Annual Mileage 10000 to reach Step 2.

## Step 3 @verifies ac-11, ac-13

On Step 2 'Enter Insurant Data', enter First Name {{valid_first_name}}, Last Name {{valid_last_name}}, Date of Birth {{future_birth_date}}, select Male and then Female, enter Street Address {{valid_street_address}}, Country Germany, Zip Code {{valid_zip_code}}, City {{valid_city}}, Occupation Employee, leave the remaining fields unchanged, then assert the future Date of Birth is rejected or visibly flagged invalid and only Female remains selected.
