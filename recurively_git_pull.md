prompt:  
```write me a bash script that when ran in one folder will look one folder down and do a git pull on every folder ```

https://chatgpt.com/share/dcb311d7-db10-42aa-9db5-ff0fff864781  

```#!/bin/bash

# Ensure the script is executed in the desired directory
current_dir=$(pwd)
echo "Running git pull in all subdirectories of: $current_dir"

# Loop through each directory one level down
for dir in */; do
    if [ -d "$dir" ]; then
        # Change to the directory
        cd "$dir"
        
        # Check if it's a git repository
        if [ -d ".git" ]; then
            echo "Running git pull in $dir"
            git pull
        else
            echo "$dir is not a git repository"
        fi
        
        # Return to the original directory
        cd "$current_dir"
    fi
done

echo "Completed git pull in all subdirectories."
```
