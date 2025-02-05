# MongoDB $inc Operator Unexpected Behavior with Negative Increments

This repository demonstrates an uncommon error related to the MongoDB `$inc` operator when used with negative increments.  The issue arises from improper handling of negative increments in certain scenarios, potentially leading to unexpected results or data inconsistencies.

## Bug Description

The `$inc` operator is typically used to increment a numeric field. However, when attempting to decrement a field using a negative value with `updateOne` and the field is not yet initialized, it behaves unexpectedly. Instead of creating the field and setting it to the negative value, no change will occur at all.

## Bug Reproduction

1.  Ensure a collection named `counters` exists (or create one).  This collection should hold documents with an `_id` field and a `sequence` field (which might not initially be present in the document).
2.  Attempt to decrement the `sequence` field using the provided JavaScript code snippet in `bug.js`.
3.  Observe that if the `sequence` field is not yet present, no change occurs; the document remains unmodified.  This differs from the expected behavior of initializing and setting the `sequence` to the negative value.

## Solution

The solution involves using the `$setOnInsert` operator in conjunction with `$inc` to address the problem. This ensures that the field is properly initialized if it doesn't exist and then incremented (or decremented) as intended.

## How to Use

1. Clone the repository
2. Run `bug.js` to reproduce the bug.
3. Then run `bugSolution.js` to see the solution
