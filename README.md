# 2-2-PROJECTS
# OS UNIBENCH PROJECT
#!/bin/bash

# Function to check the user's guess against the actual number of files
check_guess() {
    local guess=$1
    local actual=$2
    if [ $guess -lt $actual ]; then
        echo "Your guess is too low. Try again."
        return 1
    elif [ $guess -gt $actual ]; then
        echo "Your guess is too high. Try again."
        return 1
    else
        echo "Congratulations! You guessed the correct number of files: $actual"
        return 0
    fi
}

# Count the number of regular files in the current directory
file_count=$(ls -l | grep ^- | wc -l)

# Main loop to prompt user for guesses
echo "Welcome to the Guessing Game!"
echo "How many files are in the current directory?"
while true; do
    echo -n "Enter your guess: "
    read user_guess
    # Validate that the input is a number
    if [[ ! $user_guess =~ ^[0-9]+$ ]]; then
        echo "Please enter a valid number."
        continue
    fi
    # Call the check_guess function
    check_guess $user_guess $file_count
    # Exit loop if guess is correct (return code 0)
    if [ $? -eq 0 ]; then
        break
    fi
done

# End of program
exit 0
