---
assurance:
  id: t-4
  base: sha256:69fa97d00b155390d9a5bfc1c144ee16e750cf912cdc8e3ee25095781cfc0a9a
---
# Retain Step 1 vehicle data on back-navigation and reset on category switch

> Prove backward navigation from Step 2 preserves entered vehicle data, and that switching vehicle category after the journey has started resets the wizard to Step 1 for the newly chosen category.

## Step 1

Open https://sampleapp.tricentis.com/101/index.php in a fresh browser session.

## Step 2 @verifies ac-8

On the landing page, select Automobile, then assert Step 1 'Enter Vehicle Data' is displayed.

## Step 3

On Step 1 'Enter Vehicle Data' for Automobile, set Make to Audi, Engine Performance (kW) to 110, Date of Manufacture to {{valid_manufacture_date}}, Number of Seats to 5, Fuel Type to Petrol, List Price to 30000, Annual Mileage to 10000, and continue to Step 2.

## Step 4 @verifies ac-22

On Step 2, choose Back to return to Step 1, then assert the previously entered Make Audi, Engine Performance 110, Date of Manufacture {{valid_manufacture_date}}, Number of Seats 5, Fuel Type Petrol, List Price 30000, and Annual Mileage 10000 are still present.

## Step 5

On Automobile Step 1 after the retained values are visible, capture baseline: the wizard is in progress in the Automobile category on Step 1 with vehicle data already entered.

## Step 6 @verifies ac-23

From that in-progress Automobile Step 1 state, switch the vehicle category to Truck, then assert Step 1 'Enter Vehicle Data' is shown for Truck and the flow has reset to the new category's Step 1 rather than staying in the Automobile journey.
