#!/bin/bash

# Define all permutations of 5 numbers (0 1 2 3 4)
numbers=( $(seq 0 4) )
permutations=$(perl -MAlgorithm::Permute -E 'permute { say "@_" } @ARGV' "${numbers[@]}")

# Initialize counters
total=0
max_ops=0
failed=0

echo "Testing all 120 cases for 5 numbers..."

# Loop through each permutation
for perm in $permutations; do
    # Run push_swap and count operations
    ops=$(./push_swap $perm | wc -l)

    # Check if push_swap correctly sorts the stack
    result=$(./push_swap $perm | ./checker $perm)
    
    if [ "$result" != "OK" ]; then
        echo "❌ Failed on: $perm"
        ((failed++))
    else
        echo "✅ $perm -> $ops ops"
    fi

    # Track max operations
    if [ "$ops" -gt "$max_ops" ]; then
        max_ops=$ops
    fi

    ((total++))
done

echo "----------------------------------"
echo "Total tested: $total"
echo "Failed cases: $failed"
echo "Max operations: $max_ops"
echo "----------------------------------"

if [ "$failed" -gt 0 ]; then
    echo "❌ Some cases failed!"
else
    echo "✅ All cases passed!"
fi
