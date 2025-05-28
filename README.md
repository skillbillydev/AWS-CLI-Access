# AWS CLI Access

One of the ways you can access your AWS account through the command-line is by making use of [access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html). These credentials use an access key and secret access key for authentication. In a sense, the access key is like your username for logging in, and your secret access key is essentially your password. If you have the access key but not the secret access key, then you can't log in. Because of this, when you generate the keys, AWS gives you one chance to download the pair, and you must store them securely. You will be able to view the access key at any time, but if you ever lose access to the *secret* key, you will need to rotate the keys with a fresh pair and update your profile accordingly. 

It is **highly recommended** that you rotate your keys periodically for security. By doing so, even if someone is accessing your account in a subtle manner, the newly generated access key will remove their ability to authenticate to your account.

## Creating an IAM User for CLI Access

Although long-term credentials are not the absolute most secure way to interface with AWS, a solution you can use while creating projects such as this one is to create an IAM user and assign it least privilege access depending on your use case. Since this isn't a production AWS account, I have created a user and assigned it the necessary permissions to make changes through the command line rather than using the web interface. Once learned, the command line can be a much quicker way to make changes to your account without hopping through multiple pages, which can slow you down tremendously in a production environment.

### Step 1: Verify IAM Permissions

1. Log into your AWS IAM User account.
2. Ensure that you have the proper permissions to create access keys.
3. Search for **IAM** in the service menu in the top-left corner and select it from the dropdown menu.
4. Click on **Users**, then your username.
5. From there, you will be able to see what permissions your user profile has.

### Step 2: Create an Access Key

1. Select your **Username** in the top-right corner of the screen to access the dropdown menu.
2. Select **Security Credentials**, then scroll down until you find the **Access Keys** section.
3. Click **Create access key** to begin the process.

### Step 3: Configure the Key for CLI Access

1. Choose **Command Line Interface (CLI)** as the purpose of the key.
2. Read over other use cases for access keys to familiarize yourself.
3. Check the confirmation box after reading the warning prompt, then click **Next**.

### Step 4: Naming Your Key Properly

1. AWS does not require a description, but naming your key clearly identifies its purpose.
2. Use a description such as: `Local CLI Access - xxusernamexx`.
3. Click **Create access key**.

### Step 5: Save Your Access Keys

1. **IMPORTANT:** Do *not* continue forward without saving these keys!
2. AWS only allows you to view the secret access key **once**.
3. Download the keys as a `.csv` file.
4. Name the file logically for clarity in the future.
5. Click **Done**.

## Installing AWS CLI

1. Visit the [AWS Command Line Interface installation page](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
2. Find the version appropriate for your OS.
3. Download and install the package.
4. For Windows users, press `Win + R`, type `cmd`, and open the **Command Prompt**.
5. Run the command:

    ```sh
    aws
    ```

    If installed correctly, you should see: `"aws: error: the following commands are required: command"`.

## Configuring AWS CLI with Access Keys

1. Run:

    ```sh
    aws configure --profile <profile-name>
    ```

    Replace `<profile-name>` with a logical name for your IAM User.

2. Enter your **access key** from the CSV file.
3. Enter your **secret access key**.
4. Select your **region** (e.g., `us-east-1`).
5. Choose the output format (`json`, `text`, `table`). Leave blank for default (`json`).

## Verify AWS CLI Configuration

1. Run:

    ```sh
    aws s3 ls --profile <yourprofilename>
    ```

    If configured correctly, you should see a blank output unless your IAM User has access to an S3 bucket.

---

Now, based on your permissions, you can manage your account from the command line, saving you time and energy. It’s going to be an incredible undertaking to learn to use the CLI full-time, but once you do, your productivity will skyrocket (and you'll look cool, too!).
