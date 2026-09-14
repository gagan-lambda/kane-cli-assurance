---
assurance:
  id: t-7
  base: sha256:a67da9625dbfa2039bbd9464369adf23b1739df171e1019c2f96146867782d09
---
# Show all vehicle categories and enter Step 1 from each selection

> Prove the landing page exposes the full vehicle-category set and that choosing any listed category enters Step 1 of the quote wizard.

## Step 1

Open https://sampleapp.tricentis.com/101/index.php in a fresh browser session.

## Step 2 @verifies ac-7

On the landing page, inspect the vehicle-category choices, then assert the set is exactly Automobile, Truck, Motorcycle, and Camper.

## Step 3 @verifies ac-8, ac-21

From the landing page, select Automobile, then assert Step 1 'Enter Vehicle Data' is displayed and Automobile is visually indicated as the active category in the navigation.

## Step 4

Return to https://sampleapp.tricentis.com/101/index.php.

## Step 5 @verifies ac-8, ac-21

From the landing page, select Truck, then assert Step 1 'Enter Vehicle Data' is displayed and Truck is visually indicated as the active category in the navigation.

## Step 6

Return to https://sampleapp.tricentis.com/101/index.php.

## Step 7 @verifies ac-8, ac-21

From the landing page, select Motorcycle, then assert Step 1 'Enter Vehicle Data' is displayed and Motorcycle is visually indicated as the active category in the navigation.

## Step 8

Return to https://sampleapp.tricentis.com/101/index.php.

## Step 9 @verifies ac-8, ac-21

From the landing page, select Camper, then assert Step 1 'Enter Vehicle Data' is displayed and Camper is visually indicated as the active category in the navigation.
