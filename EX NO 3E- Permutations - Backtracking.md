
# EX 3E Generate Permutations using Backtracking
## Date:
## Aim:
To write a Java program to for given constraints. Given an array nums of distinct integers, return all the possible Permutation. You can return the answer in any order.

**Example:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

## Algorithm
1. **Start & Prepare** — Read the input array `nums`. Create an empty list `ans` to hold permutations and a temporary list `curr` for the current permutation under construction.  
2. **Backtracking Entry** — Call the recursive function `backtrack(curr, ans, nums)`.  
3. **Complete Permutation Check** — If `curr.size() == nums.length`, add a copy of `curr` to `ans` and return.  
4. **Try Candidates** — For each number `num` in `nums`, if it is not already in `curr`, append it to `curr`, recursively call `backtrack`, then remove the last element to backtrack and try the next candidate.  
5. **Return Results** — After exploring all possibilities, `ans` contains all permutations; return and print it.

## Program:
```
Program to implement permutations

Developed by: Krithick Vivekananda
Register Number: 212223240075

import java.util.*;

public class Solution {

    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        backtrack(new ArrayList<>(), ans, nums);
        return ans;
    }

    public void backtrack(List<Integer> curr, List<List<Integer>> ans, int[] nums) {
        if (curr.size() == nums.length) {
            ans.add(new ArrayList<>(curr));
            return;
        }

        for (int num : nums) {
            if (!curr.contains(num)) {
                curr.add(num);
                backtrack(curr, ans, nums);
                curr.remove(curr.size() - 1);
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Accept input in the form: nums = [1,2,3]
        //System.out.print("Input: ");
        String inputLine = scanner.nextLine().trim();

        // Extract the array part from the string
        inputLine = inputLine.replaceAll(".*\\[|\\].*", ""); // get content inside brackets
        String[] parts = inputLine.split(",");

        int[] nums = new int[parts.length];
        for (int i = 0; i < parts.length; i++) {
            nums[i] = Integer.parseInt(parts[i].trim());
        }

        // Generate permutations
        Solution solution = new Solution();
        List<List<Integer>> permutations = solution.permute(nums);

        // Print output
        System.out.println(permutations);
        scanner.close();
    }
}
```

## Output:
<img width="1199" height="165" alt="image" src="https://github.com/user-attachments/assets/d84c8429-ca9e-46d6-9dc8-831c1277bf17" />

## Result:
The program was successfully implemented and the expected output is verified.
