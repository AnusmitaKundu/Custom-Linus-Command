# Custom-Linus-Command

#!/bin/bash

# internsctl - Custom Linux command for managing interns
# Version: v2.1.0

# Usage message
usage() {
    echo "Usage: internsctl [options]"
    echo "Options:"
    echo "  -h, --help     Display this help message"
    echo "  -v, --version  Display the version"
    # Add more options and their descriptions as needed
}

# Version message
version() {
    echo "internsctl version v2.1.0"
}

# Main function to handle command-line arguments
main() {
    case "$1" in
        -h|--help)
            usage
            ;;
        -v|--version)
            version
            ;;
        *)
            echo "Error: Unknown option: $1"
            usage
            exit 1
            ;;
    esac
}

# Entry point
main "$@"


#!/bin/bash

# Command version
VERSION="v0.1.0"

# Function to display usage guidelines
usage() {
    echo "Usage: internsctl file getinfo [options] <file-name>"
    echo "Options:"
    echo "  --size, -s            Print file size"
    echo "  --permissions, -p     Print file permissions"
    echo "  --owner, -o           Print file owner"
    echo "  --last-modified, -m   Print last modified time"
}

# Function to get file size
get_size() {
    stat -c %s "$1"
}

# Function to get file permissions
get_permissions() {
    stat -c %A "$1"
}

# Function to get file owner
get_owner() {
    stat -c %U "$1"
}

# Function to get last modified time
get_last_modified() {
    stat -c %y "$1"
}

# Main function to handle command-line options
main() {
    if [ "$#" -lt 2 ]; then
        echo "Error: File name not provided."
        usage
        exit 1
    fi

    file="$2"

    case "$1" in
        --size|-s)
            get_size "$file"
            ;;
        --permissions|-p)
            get_permissions "$file"
            ;;
        --owner|-o)
            get_owner "$file"
            ;;
        --last-modified|-m)
            get_last_modified "$file"
            ;;
        --help)
            usage
            ;;
        --version)
            echo "internsctl version $VERSION"
            ;;
        *)
            echo "Error: Unknown option: $1"
            usage
            exit 1
            ;;
    esac
}

# Entry point
main "$@"
