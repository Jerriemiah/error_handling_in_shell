### **Mini Project - Error Handling in Shell Scripting**

Error handling is a critical component of shell scripting that ensures scripts execute reliably and efficiently. It involves anticipating potential failures—such as incorrect inputs, resource unavailability, or unexpected system behavior—and incorporating mechanisms to manage these situations. By leveraging **conditional statements** (`if-else`), **loops**, and **exit status codes** (`$?`), we can detect, handle, and provide informative feedback when errors occur. 

One practical example is managing **AWS S3 bucket creation**. Creating a bucket without checking if it exists can lead to unnecessary failures. A **robust script** should first verify whether the bucket already exists before attempting creation. If the bucket is present, the script should notify the user instead of trying to recreate it. This enhances efficiency, prevents redundant operations, and ensures seamless execution.

### **Hands-on Implementation: Error Handling in AWS S3 Bucket Creation**

Here’s an example shell script implementing error handling when creating S3 buckets:

```sh
#!/bin/bash

# Function to create S3 buckets for different departments
create_s3_buckets() {
    company="datawise"
    departments=("Marketing" "Sales" "HR" "Operations" "Media")

    for department in "${departments[@]}"; do
        bucket_name="${company}-${department}-Data-Bucket"

        # Check if the bucket already exists
        if aws s3api head-bucket --bucket "$bucket_name" &>/dev/null; then
            echo "S3 bucket '$bucket_name' already exists."
        else
            # Attempt to create the S3 bucket
            aws s3api create-bucket --bucket "$bucket_name" --region your-region
            if [ $? -eq 0 ]; then
                echo "S3 bucket '$bucket_name' created successfully."
            else
                echo "Failed to create S3 bucket '$bucket_name'."
            fi
        fi
    done
}

# Execute the function
create_s3_buckets
```

### **Key Features of This Script**
- **Error Prevention:** The script checks if a bucket exists before trying to create it.
- **Exit Status Handling (`$?`):** Determines if the bucket creation was successful or failed.
- **Looping Mechanism:** Iterates through different departments, ensuring automation.
- **Informative Output:** Provides meaningful messages to the user about success or failure.

By implementing this **hands-on approach**, the script becomes more resilient, reducing failures and improving automation efficiency. This fulfills the **instructor's requirement** for practical implementation with error handling, control flow, and validation.
 
