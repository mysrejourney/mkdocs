# Exercises from Hackerrank - Python


### Exercise # 1

In this challenge, the user enters a string and a substring. 
You have to print the number of times that the substring occurs in the given string. 
String traversal will take place from left to right, not from right to left.

**NOTE:** String letters are case-sensitive.

**Input Format**



The first line of input contains the original string. The next line contains the substring.

**Constraints**

```Python
1 <= len(string) <= 200
```
Each character in the string is an ascii character.

**Output Format**

Output the integer number indicating the total number of occurrences of the substring in the original string.

**Sample Input**

```Python
ABCDCDC
CDC
```

**Sample Output**

```Python
2
```

### Solution  # 1

```Python
#######################################################################################################################################
# LOGIC: 
# You need to slice the given string with the length of substring from starting and compare the sliced string with given substring.
# If it matches, increase the count. Else, move the next position of the string and start slicing until it reaches the difference of both string length

# TO DO:
# 1. Initiate occurance count as 0. Get the length of both strings
# 2. Find out the difference of these length. You need to loop from 0 to this length
# 3. Slice the string from 0 to length of the substring.
# 4. Compare it with substring. If matches, increase the occurance count. Else, run the loop again
# 5. Now, get the slice from position 1 to length of the substring and do the step 4. This will continue until the loop ends
# 6. Return the occurance count.

#######################################################################################################################################

#######################################################################################################################################
# Function name: count_substring
# Arguments: given_string, given_sub_string
# Return: number_of_occurrance
# Description : Slice / Compare / Return

#######################################################################################################################################

def count_substring(given_string, given_sub_string):
	number_of_occurrance = 0
	# Find the length of the given inputs
	length_of_string = len(given_string) # 7
	length_of_sub_string = len(given_sub_string) # 3

	# Find the difference of length of the given inputs
	difference = length_of_string - length_of_sub_string # 4
	
	# Loop through
	for position in range(0, difference + 1): # 0 1 2 3 
		# Slice the string with length of the substring
		print(f"{given_string[position : position + (difference - 1)]}")
		# Compare the slice with substring
		if (given_string[position : position + (difference - 1)] == given_sub_string): # 
			number_of_occurrance += 1 # Increase the count
	
	return number_of_occurrance # return the count


if __name__ == "__main__":
	# Get the strings
	given_string = input(f"Enter your string : " ) # ABCDCDC
	given_sub_string = input(f"Enter your substring to find : ") # CDC

	# Call the function
	count = count_substring(given_string, given_sub_string)

	# Print the result
	print(f"Give substring : {given_sub_string} is occurred {count} times in the given string : {given_string}")

```

![py_sln_1.png](../assets/py_sln_1.png)



