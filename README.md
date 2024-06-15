# Linux_Shell_Scripting

# Multiplication Table Generator

## Project Description

This project involves creating a Bash script that generates a multiplication table for a number entered by the user. The script offers both a full multiplication table (1 to 10) and a partial table based on a specified range. The project aims to practice using loops, handling user input, and applying conditional logic in Bash scripting.

## Features

- User input for the number to generate the multiplication table.
- Choice of generating a full table or a partial table.
- Input validation for number and range inputs.
- Clear and readable output formatting.
- Enhanced user interaction with the option to generate another table without restarting the script.

## Script Flow

1. Prompt the user to enter a number for the multiplication table.
2. Ask if they want a full table or a partial table.
   - If partial, prompt for the start and end numbers of the range.
3. Validate the range inputs and handle invalid or out-of-bound entries.
4. Generate and display the multiplication table according to the specified range.
5. Provide clear output formatting for ease of reading.
6. Option to repeat the program for another number without restarting the script.

## Example Outputs

### Full Multiplication Table

![Script_1](/Images/Script_1.png)

### Partial Multiplication Table

![Script_2](/Images/Script_2.png)


### Handling Invalid Range

![Script_3](/Images/Script_3.png)

The following is the code for the script:

```

## Script Code

```bash
#!/bin/bash

# Function to display the full multiplication table
display_full_table() {
  local num=$1
  echo "The full multiplication table for $num:"
  for i in {1..10}; do
    echo "$num x $i = $((num * i))"
  done
}

# Function to display a partial multiplication table
display_partial_table() {
  local num=$1
  local start=$2
  local end=$3
  echo "The partial multiplication table for $num from $start to $end:"
  for ((i = start; i <= end; i++)); do
    echo "$num x $i = $((num * i))"
  done
}

# Function to validate if input is a number
is_number() {
  [[ $1 =~ ^[0-9]+$ ]]
}

# Main script
while true; do
  # Prompt user for a number
  read -p "Enter a number for the multiplication table: " num

  # Validate if input is a number
  if ! is_number "$num"; then
    echo "Invalid input. Please enter a valid number."
    continue
  fi

  # Ask if user wants a full table or a partial table
  read -p "Do you want a full table or a partial table? (Enter 'f' for full, 'p' for partial): " choice

  if [[ $choice == "f" ]]; then
    display_full_table "$num"
  elif [[ $choice == "p" ]]; then
    # Prompt for start and end range
    read -p "Enter the starting number (between 1 and 10): " start
    read -p "Enter the ending number (between 1 and 10): " end

    # Validate range inputs
    if is_number "$start" && is_number "$end" && ((start >= 1 && start <= 10)) && ((end >= 1 && end <= 10)) && ((start <= end)); then
      display_partial_table "$num" "$start" "$end"
    else
      echo "Invalid range. Showing full table instead."
      display_full_table "$num"
    fi
  else
    echo "Invalid choice. Showing full table instead."
    display_full_table "$num"
  fi

  # Ask if user wants to repeat the program
  read -p "Do you want to generate another table? (y/n): " repeat
  if [[ $repeat != "y" ]]; then
    break
  fi
done
```
